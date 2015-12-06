---
layout: post
title:  "Problem Description and State of the Art"
date:   2015-04-12 21:47:00
excerpt_separator: <!--more-->
---

This thesis is part of the over-arching project of crafting an end-user-friendly client-application for the [Web of Needs](http://www.webofneeds.org/)([related publications](http://sat.researchstudio.at/en/web-of-needs)), short WoN. It is a set of protocols (and reference implementations) that allow posting things like supply and demand (e.g. "I have a couch to give away") online on an arbitrary data server (called WoN-Node). These documents, called "needs", get discovered by a matching-service that notifies the owners of these needs (e.g. when the matcher finds someone that needs the couch offered). The protocols then allow for chatting (or other transactions) between the owners. This thesis focusses mainly on viewing and editing these needs. These documents get published in a special type of syntax called [Resource Description Framework](http://www.w3.org/RDF/) (RDF). It allows to combine data from multiple sources all over the web, which is the reason why it was chosen for the Web of Needs project.
<!--more-->

However, as it's a formalized markup-language, it's not suited for viewing or authoring by people without the required know-how about it's syntax. As such most people using the Web of Needs will not be able to directly work with it and need the abstraction of a graphical user interface (GUI).

To move on to the key problem: The Web of Needs is intended as a domain-open platform, enabling everything from gifting used clothes over finding a tennis partner to discovering a job with a matching profile. This means there can't be a one-size-fits-it-all GUI. It needs to be adapted to the peculiarities and requirements of the tasks people are trying to accomplish via it. This, however, means that there will be a lot of effort required to build these interfaces. To facilitate that, two general approaches present themselves: A) to split the GUIs into smaller pieces (widgets) that can be reused and recombined if it's easy enough to find the right one. B) to make combining these widgets more approachable (especially for non-programmers), thus increasing the number of people who can contribute to the task (see [End-User-Programming, EUP](http://mitpress.mit.edu/books/small-matter-programming))


---

## Old Version

(DISCLAIMER: no liability assumed for any harmed sense of grammar / spelling / stuff making sense. this is alpha-stage text written with the intent to have a basis for feedback)

RDF is nice. RDF is good and very useful. RDF in it's many variant syntaxes allows to easily reference and combine data from different sources, different services, different providers. However, reading RDF-code can mildly confusing for developers who come across it the first time and downright deterent to anyone who's not used to read code at all (read: most people benefitting from RDF-based technologies or browsing the internet). The problem is even worse for authoring RDF. Due to the number of different yet often-times
similiar ontologies picking the right one and the right syntax is a task that requires a lot of familiarity with the semantic web (or a corresponding amount of initial research and trial-and-error to become aquainted with what's out there). Even after this initial stage authoring isn't effortless as the syntax has to be strictly enforced (in comparison to writing non-machine-readable/normal text readable). The aid of an IDE with auto-completion or predicate-lookup can help to at least forego the
need to remember all predicates for a given type of subject (e.g. [rdfedit](https://github.com/suchmaske/rdfedit) which uses [Sindice](http://sindice.com/) for the lookup). However even in this case you still need to input data in the form of triples which requires a significant shift in thinking about the content to be penned down (in comparison to more natural, graphical representations). Also it exposes the complexity and structure of coding, respectively at least parts of the syntax (i.e. URIs) to the author which is deterrent for non-programmers who at best are used to classical forms.

Thus a graphical interface of one sort or another immensely helps with viewing/editing RDF-data - especially if it employs the representative power of (interactive) visualizations instead of forms/tables.

In general there's two kinds of GUIs used a the moment: On the one hand there's generic data-browsers like e.g. [XYZ](#) <!-- [Tabulator](http://www.w3.org/2005/ajar/tab)
still has queries, <http://rhizomik.net/html/rhizomer/> has visus,
<https://code.google.com/p/ontology-browser/>
the browser listed in the pivot paper
Longwell, IsaViz and Haystack
-->
, which usually offer some form of tree or graph based exploration. However, due to their generality they stay relatively abstract, technical and close to the underlying data-structure in their representation. This makes them only usable to experts in the field. On the other hand there's specialized, hand-crafted, stand-alone applications which usually draw from specific, predefined data-sources and need to be substantially adapted for every new data-source they want to be connected too. There's little in the way of reusable widgets that connect to specific data-source, let alone that can deal with generic sources. <!-- {DO RESEARCH ON THIS. Maybe there's at least some generic components} -->

Also, there's [Pivot](#) that tries provide some interaction between the GUIs, not at widget but at application level, by standardizing a protocol between them (e.g. you could select countries in a map-application and let the respective gross domestic products be visualized in a linked economical statistics application)

As for developing RDF-based applications and especially user interfaces:

Reusability of code not only is important for reducing the development effort, but in the latter case also help people learn the interaction language / workflows of the GUI.

Usually widgets are implemented in and thus bound to specific frameworks/libraries (e.g. [jQuery](https://jquery.com/), [Angular](https://angularjs.org/), [React](https://facebook.github.io/react/index.html),...). As a consequence these have to be served as well, increasing the page-load time. In the case of libraries at least they tend to be composable (i.e. you can serve a [React](https://facebook.github.io/react/index.html)-component next to a [jQuery](https://jquery.com/)-widget). In the case of full client-side frameworks such as [Backbone](www.backbonejs.org), [Angular](https://angularjs.org/), [Ember](www.emberjs.com) or RDF-centric, static-templating [Fresnel](http://www.w3.org/2005/04/fresnel-info/manual/) they're mutually exclusive. <!--{REF/EXAMPLE NEEDED}--> Thus every widget build with one of these has to reimplemented in the next. By extend the same holds true for the data-binding layer between RDF and GUI, which needs to be adapted to the peculiarities of these frameworks again and again. Thus, to get good reusability, any any solutions should favor vanilla, standard-conform javascript over libraries over full frameworks. Also for the sake of good page-load performance, the less code to be delivered, the better.

Even assuming a slim, reusable component there's still the need for a developer to sit down, include the component into the build and connect it to the endpoint(s) for the data it should display or allow editing of. Whenever people without the technical knowledge come across RDF for which no developer has implemented or included a visual representation, they're out of luck. Even when there might be suited representations to be easily found elsewhere (e.g. dedicated [jQuery](https://jquery.com/) widgets), feeding them from the data-sources will still require programming skills and manual fine-tuning. A more usable solution might automatically find and display a fitting visual representation instead of the raw RDF, if there's one in existence.

EDIT: Turns out, there's a wide variety of mashup tools out there, that do an acceptable job at filtering, combining and displaying data from multiple sources, even for non-programmers. A small list of examples include: [Microsoft Popfly](#)(discontinued), [Yahoo Pipes](#) and [LinkedWidgets](http://linkedwidgets.org). The ones listed all offer a graph-based editor to connect different, preconfigured data-sources and widgets. In contrast, [Naturalmash](http://naturalmash.com) ([video](https://www.youtube.com/watch?feature=player_embedded&v=SMAwIFL45GA), [paper](http://design.inf.usi.ch/sites/default/files/biblio/naturalmash-icwe2011phd.pdf)) takes a slightly different approach using English sentences with blanks for input parameters, thus providing a very approachable end user programming (EUP) experience. However it also comes with a fixed set of preconfigured sources and widgets.

<!--

devprobs: atm domain-specific, rapidly shifting user-needs (e.g. in data-analysis)

user's probs: (i) find data, (II) tech skills to access, (iii) processing & integrating

In line with the Linked Data
paradigm, end user tools should be:

* based on openness
* foster reusabil-
ity
* and be flexible enough to handle arbitrary data sources.

with Open Data sources:

* access
* process
* integrate
* visualize

"end user programming" to reduce need for devs (?)

[An API for APIs](http://api-portal.anypoint.mulesoft.com/programmable-web/api/programmable-web-api)
programmableweb.com

why we find editing so important - won

include overview over existing mashups & end-user-programming techniques

@linkedwidgets:

* improve design (to produce more user-friendly guis)
* rewrite to use webcomponents instead of iframes?
* conditional forms? (only show field iff onto has it. or within onto: only allow specifying "recurs in" if there's a start date.)
* editing & publishing!
  * user doesn't start with: "i want to publish rdf" but "I want to find sthg at the WoN"
  * the newbie also won't start with "i have this onto"
  * rdf publishing should happen in the background
  * the system may make demands to improve results (interaction cycle)
  * very advanced users with a firm grasp of why rdf is necessary (and devs of companies using the WoN) will craft GUIs and should have an as easy as possible job doing that (or not be required -> auto-gen an 'okay' gui, though where does the onto come from? -> reduce dev effort to selecting a few ontos?)

hosting happens on own platforms, it's only a repo-server (with urls to actual widgets)

popfly (discontinued)
yahoo pipes (small / partly disfunctional examples)
linkedwidgets.org



-->
<!--

effect for society: more value from existing data sets without a lot of extra development effort

why did i choose it?

bringing data along?

reference to Igor's paper

To summarize...what it needs is sthg that...[solves x, y and z] provides:

* user-centered viewing and editing interface, e.g. interactive visualisations
* code reusability
* reduction of required knw of which ontos are out there for any developers
* automatic discovery for data that has not been wrapped into GUIs yet by devs
* stays close to the w3c standard
* has no additional dependencies or at worst a library that's as small as possible
-->

## Example

Consider for instance a situation where...


<!--
* social network, e.g. twitter
    * persons
    * relationships
    * geo-tags
* ecommerce ordering stuff
    * foaf
    * address
    * logistics-data
-->
<!--
* stuff that's implemented relatively often
    * date-pickers
        * there's libraries here
        * these don't do rdf
        * and need to be included manually
        * and connected manually to the app's model (<- easier with rdf; just push it (?))
    * calender views
    * maps
        * a lot of geo-spatial data that's still not readily available in maps (e.g. find an address string somewhere, show the map to it)
    * address information
    * date/time information
        * auto-localisation


* meta: 2 examples that will be going examples through-out the thesis
  * foaf:person? (for comparison with fresnel?) -> business-card, entering data into sign-up-forms
  * one of the comps should be an interactive visualisation(!)
    * view and edit a frequently occurring data-source
    * geo-spatial data? a map.  viewing (yes!), editing(?), selecting stuff on it(yes!) (e.g. pick a particular [grundparzelle], a particular road, a particular building,...)
    * start with simple example (becomes running example through out thesis)-->



<!--
repo-server: serve template-function that takes json-ld object and renders to html? (can be rendered in webapp on server or client) 
ad hoc guis
paste data url, show as gui
browser plugin that does that automatically
drag & drop composition
pick from fitting widgets, build-your-own-form/gui/representation
-->
