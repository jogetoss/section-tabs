# Description

The Section Tab is a Form Element plugin that changes the display of a form's sections, originally from top to bottom, to a horizontal tabs type display.

# Getting Help

JogetOSS is a community-led team for open source software related to the [Joget](https://www.joget.org) no-code/low-code application platform.
Projects under JogetOSS are community-driven and community-supported.
To obtain support, ask questions, get answers and help others, please participate in the [Community Q&A](https://answers.joget.org/).

# Contributing

This project welcomes contributions and suggestions, please open an issue or create a pull request.

Please note that all interactions fall under our [Code of Conduct](https://github.com/jogetoss/repo-template/blob/main/CODE_OF_CONDUCT.md).

# Licensing

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

NOTE: This software may depend on other packages that may be licensed under different open source licenses.

## Regression repro app

`APP_SectionTabsRepro-1.jwa` is a minimal app for checking Section Tabs against circular configurations.

- **Bad (self-referencing tabs)** — a Section Tabs element placed inside `section_a` that lists `section_a` (and a missing `section_b`), twice. Before this fix (8.0.0 `setParent` re-parents the ancestor section's children; 9.0.5/9.0.6 instead drop the whole section) the parent chain becomes circular and the request spins forever in `FormUtil.findRootForm`. With the fix the element is ignored and the form renders normally.
- **Good (own-section tabs)** — Section Tabs in its own section wrapping two earlier sections. Must still render as two tabs.

Note that sections are parsed in order, so the sections listed in `sections` must appear **before** the Section Tabs element in the form.
