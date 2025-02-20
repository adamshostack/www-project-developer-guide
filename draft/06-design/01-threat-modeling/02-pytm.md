---

title: Threat Modeling with pytm
layout: col-document
tags: OWASP Developer Guide
contributors: Jon Gadsden
document: OWASP Developer Guide
order: 612

---

{% include breadcrumb.html %}

### 4.1.2 Pythonic Threat Modeling

The OWASP [Pythonic Threat Modeling (pytm)][pytmproject] project is a framework for threat modeling and its automation.
The goal of pytm is to shift threat modeling to the left, making threat modeling more automated and developer-centric.

Pytm is an OWASP Lab Project with a community of contributors creating [several releases][pytmreleases].

#### What is pytm?

Pytm is a Java library that provides programmatic way of threat modeling;
the application model itself is defined as a python3 source file and follows Python program syntax.
Findings are included in the application model python program with threats defined as rows in an associated text file.
The threat file can be reused between projects and provides for accumulation of a knowledge base.

Using pytm the model and threats can be programmatically output as a [dot][graphvizdot] data flow diagram
which is displayed using [Graphviz][graphviz], an open source graph visualization software utility.
Alternatively the model and threats can be output as a [PlantUML][plantuml] file which can then be displayed,
using Java and the PlantUML `.jar`, as a sequence diagram.

If a report document is required then a pytm script can output the model, threats and findings as markdown.
Programs such as [pandoc][pandoc] can then take this markdown file
and provide the document in various formats such as PDF, ePub or html.

#### Why use it?

The pytm development team state that traditional threat modeling often comes too late in the development process,
and sometimes may not happen at all.
In addition, creating manual / diagrammatic data flows and reports can be extremely time-consuming.
These are very good points, and pytm attempts to get threat modeling to 'shift-left' in the development lifecycle.

Many traditional threat modeling tools such as OWASP Threat Dragon provide
a graphical way of creating diagrams and entering threats.
These applications store the models as text, for example JSON and YAML, but the main entry method is via the application.

Pytm is different - the primary method of creating and updating the threat models is through code.
This source code completely defines the model along with its findings, threats and remediations.
Diagrams and reports are regarded as outputs of the model; not the inputs to the model.
This makes pytm a powerful tool for describing a system or application, and allows the model to be built up over time.

This focus on the model as code and programmatic outputs makes Pytm particularly useful in automated environments,
helping the threat model to be built in to the design process from the start,
as well as in the more traditional threat modeling sessions.

#### How to use it

The best description of how to use pytm is given in chapter 4 of the book
[Threat Modeling: a practical guide for development teams][TMchap4]
which is written by two of the main contributors to the pytm project.

Pytm is code based within a program environment, rather than run as a single application,
so there are various components that have to be installed on the target machine to allow pytm to run.
At present it does not work on Windows, only Linux or MacOS, so if you need to run Windows then use a Linux VM
or follow the instructions to create a Docker container.

The following tools and libraries need to be installed:

* Python 3.x
* [Graphviz][graphvizdot] package
* Java, such as OpenJDK 10 or 11
* the [PlantUML][plantumljar] executable JAR file
* and of course pytm itself: clone the [pytm project repo][pytmrepo]

Once the environment is installed then navigate to the top directory of your local copy of the project
Follow [the example][pytmexample] given by the pytm project repo and run the suggested scripts
to output the data flow diagram, sequence diagram and report:

```text
mkdir -p tm
./tm.py --report docs/basic_template.md | pandoc -f markdown -t html > tm/report.html
./tm.py --dfd | dot -Tpng -o tm/dfd.png
./tm.py --seq | java -Djava.awt.headless=true -jar $PLANTUML_PATH -tpng -pipe > tm/seq.png
```

----

The OWASP Developer Guide is a community effort; if there is something that needs changing
then [submit an issue][issue060102] or a [pull request][pr] .

[graphviz]: https://graphviz.org/
[graphvizdot]: https://graphviz.org/download/
[issue060102]: https://github.com/OWASP/www-project-developer-guide/issues/new?labels=enhancement&template=request.md&title=Update:%2006-design/01-threat-modeling/02-pytm
[pandoc]: https://pandoc.org/installing.html
[plantuml]: https://plantuml.com/
[plantumljar]: https://plantuml.com/download
[pr]: https://github.com/OWASP/www-project-developer-guide/pulls
[pytmrepo]: https://github.com/izar/pytm/
[pytmproject]: https://owasp.org/www-project-pytm/
[pytmexample]: https://github.com/izar/pytm/blob/master/tm.py
[pytmreleases]: https://github.com/izar/pytm/releases
[TMchap4]: https://www.oreilly.com/library/view/threat-modeling/9781492056546/ch04.html

\newpage
