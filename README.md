# Alien6 Catalog
A currated collection of Helm charts that have been tested at Alien6 which can be directly imported in Rancher 2.x.

## Rancher Chart Structure

A Rancher chart repository differs slightly in directory structure from upstream repos in that it includes an `app version` directory. Though Rancher can use native Helm repositories as well.

A Rancher chart also has two additional files an `app-readme.md` file that provides a high level overview display in the Rancher 2.0 UI and a `questions.yml` file defining questions to prompt the user with. 

```
charts/wordpress/<app version>/
  app-readme.md            # Rancher Specific: Readme file for display in Rancher 2.0 UI
  charts/                  # Directory containing dependency charts
  Chart.yaml               # Required Helm chart information file
  questions.yml            # Rancher Specific: File containing questions for Rancher 2.0 UI
  README.md                # Optional: Helm Readme file (will be rendered in Rancher 2.0 UI as well)
  requirements.yaml        # Optional YAML file listing dependencies for the chart
  templates/               # A directory of templates that, when combined with values.yml will generate K8s YAML
  values.yaml              # The default configuration values for this chart
```
*See the upstream Helm chart [developer reference](https://docs.helm.sh/developing_charts/) for a complete walk through of developing charts.*

### Question Variable Reference

| Variable  | Type | Required | Description |
| ------------- | ------------- | --- |------------- |
| 	variable          | string  | true    |  define the variable name specified in the `values.yaml`file, using `foo.bar` for nested object. |
| 	label             | string  | true      |  define the UI label. |
| 	description       | string  | false      |  specify the description of the variable.|
| 	type              | string  | false      |  default to `string` if not specified (current supported types are string, boolean, int, enum, password, storageclass and hostname).|
| 	required          | bool    | false      |  define if the variable is required or not (true \| false)|
| 	default           | string  | false      |  specify the default value. |
| 	group             | string  | false      |  group questions by input value. |
| 	min_length        | int     | false      | min character length.|
| 	max_length        | int     | false      | max character length.|
| 	min               | int     | false      |  min integer length. |
| 	max               | int     | false      |  max integer length. |
| 	options           | []string | false     |  specify the options when the vriable type is `enum`, for example: options:<br> - "ClusterIP" <br> - "NodePort" <br> - "LoadBalancer"|
| 	valid_chars       | string   | false     |  regular expression for input chars validation. |
| 	invalid_chars     | string   | false     |  regular expression for invalid input chars validation.|
| 	subquestions      | []subquestion | false|  add an array of subquestions.|
| 	show_if           | string      | false  | show current variable if conditional variable is true, for example `show_if: "serviceType=Nodeport"` |
| 	show\_subquestion_if |  string  | false     | show subquestions if is true or equal to one of the options. for example `show_subquestion_if: "true"`|

**subquestions**: `subquestions[]` cannot contain `subquestions` or `show_subquestions_if` keys, but all other keys in the above table are supported. 

## License
Copyright (c) 2019 [Alien6](https://alien6.com)

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

[http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
