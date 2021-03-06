# Architecture

Architecture should be designed for change, and you must never make comproises that impact architecture goals negatively as architecture is by definition hard to change .

> An evolutionary architecture supports **incremental**, **guided change** as a first principle along **multiple dimensions**

## Architectural practices for evolution

![](../.gitbook/assets/principles-of-evolutionary-architecture.png)  
Source: [Patrick Kua - Goto Conference](https://www.youtube.com/watch?v=8bEsNT7jdC4&t=112s&index=57&list=WL)

### Technical Practices:

**API First**, **REST/Event Driven,** **SaaS**, **Cloud**, and **Microservices**. We’re creating APIs first before we code them, using the REST/Event Driven architectural style to ensure we’re able to scale as our department and business grows in scope, evolving our systems in parallel. Building for SaaS makes our applications ready to live on the Internet, where embracing the cloud ensures that as a modern architecture, we’re fostering innovation. Finally, our adoption of Microservices ties all these principles together in a powerful architectural style that lets us move fast while we keep our complexity low. Source: [Zalando Blog](https://jobs.zalando.com/tech/blog/radical-agility-study-notes/?gh_src=4n3gxh1)

* API First - as a plattform you care more about APIs/ business functions then the UI as the UI could be delivered by someone else using your API.

### Fitness Function are the goal and quantitative measure to evaluate the guide change

[https://medium.com/developers-writing/my-take-on-evolutionary-architecture-f761d45e75b9](https://medium.com/developers-writing/my-take-on-evolutionary-architecture-f761d45e75b9)

* Testing for "First Principles" \(basis that will be hard to correct in the long term and the negative impacts in production can only be monitored later when they stack up\) -&gt; can be de priortized for first mvp?:
  * Code Quality
  * Complexity 
  * Functionality \(easier to test and interpret where the error is on unit level but in the end only relevant on the quality level of the solution\)
* Testing "Quality" \(how good is the current solution: 
  * Real time monitoring for  \([http://benjiweber.co.uk/blog/2015/03/02/monitoring-check-smells/\](http://benjiweber.co.uk/blog/2015/03/02/monitoring-check-smells/%29\)
    * perfomormance
    * security

#### Fitness functions / SLAs Types:

* Automation \( -&gt; AI\)
* Reasonable Security
* Limited Blast Radius

## Dimentions of architectural diagramms:

* solution \(process & component\)
* implementation / technology \(frameworks\)
* production
* evolution

Tool: [plantuml](http://plantuml.com)

### Domain Diagrams

* [https://www.heise.de/developer/artikel/Domain-driven-Design-erklaert-3130720.html?seite=all](https://www.heise.de/developer/artikel/Domain-driven-Design-erklaert-3130720.html?seite=all)
* [https://docs.google.com/drawings/d/1kwtMhXe-3YLrqlLa-MoE84U-lDr-k5Z6qtlWgCuvHkk/edit](https://docs.google.com/drawings/d/1kwtMhXe-3YLrqlLa-MoE84U-lDr-k5Z6qtlWgCuvHkk/edit)

## Documentation of Architecutral Decisions

Architectural decision should be documented in a [light weight architecture decision record](https://github.com/CloudNativeTraining/architecture_decision_record). My private decision are located here in [github](https://github.com/denseidel/developer-playbook/tree/master/adr) based on this [template](https://github.com/CloudNativeTraining/architecture_decision_record/edit/master/adr_template_madr.md).

Use the [adr tool](https://github.com/npryce/adr-tools) and [MADR](https://github.com/adr/madr)

```text
brew install adr-tools
npm install madr && mkdir -p docs/adr && cp node_modules/madr/template/* docs/adr/
```

## Keep a technology overview with the Tech Radars:

* [https://zalando.github.io/tech-radar/](https://zalando.github.io/tech-radar/)
* [https://www.thoughtworks.com/de/radar](https://www.thoughtworks.com/de/radar)

## Community

* [https://jobs.zalando.com/tech/](https://jobs.zalando.com/tech/)

