
# hl7.github.io

This is the [Jekyll](https://jekyllrb.com) source code used to generate http://hl7.github.io, the developer landing site for HL7 FHIR core library projects.

## Prerequisites

You will need to have the following software installed to preview the generated website.

* Ruby version 2.5.0 or higher ([installation instructions](https://www.ruby-lang.org/en/documentation/installation/))
* Ruby Gems ([download](https://rubygems.org/pages/download))
* [GCC](https://gcc.gnu.org/install/) and [Make](https://www.gnu.org/software/make/)
* Jekyll ([installation instructions](https://jekyllrb.com/docs/installation/))

## Building this Project

### Developing locally

Navigate to the root directory of the project. The following command will make a development build of the website available at `http://127.0.0.1:4000/`

```shell
bundle exec jekyll serve
``` 

### Deploying to hl7.github.io

Once you are satisfied with your changes locally, make a [Pull Request](https://github.com/HL7/hl7.github.io/compare) to this project. If your Pull Request is approved, once it is merged into the main branch, the changes will automatically be deployed to hl7.github.io.


## Contributing

This repository and the hl7.github.io website is maintained by [David Otasek](https://github.com/dotasek/) and [Mark Iantorno](https://github.com/markiantorno) on behalf of the FHIR community.
