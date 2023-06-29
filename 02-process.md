---
jupytext:
  formats: md:myst
  text_representation:
    extension: .md
    format_name: myst
    format_version: 0.13
    jupytext_version: 1.11.5
kernelspec:
  display_name: Python 3
  language: python
  name: python3
---

(chapter02)=
# The Process of Visualizing Data

% The Process of Visualizing Data (what are possible starting points for the design; how does the process relates to human-centered design; what are existing flaws; what are possible instances)
% Reflecting on Data (what are differences between data, information, knowledge; what is cooked data; what is the difference between thick and thin data)
% Reflecting on Tasks (domain specific language, tasks consisting of actions and targets)
% Outlook: The How of Visualization Design - at a glance
% TODO: Reorganize the whole section and put the human-centered design process in the center, remove the nested model!!!


In {numref}`Chapter %s <chapter01>`, we have learned that visualization have helped people from the beginning to make sense of their environment. Before we dive deeper into data visualization, we need to build the necessary methodological foundation. For this, we already introduced human-centered design (see {numref}`01-hcdv`); however, in this chapter, I want to focus specifically on the process of visualizing data. In general, we can differentiate two motivations for visualization design: a problem-driven and a technique driven design {cite}`munzner2014visualization`. In the former case, a visualization designer tackles a real-world problem of specific users and attempt to design a solution that helps them work more effectively. Such problem can often be solved based on existing visual encoding and interaction idioms (see {numref}`01-hcdv`), thus, the main challenge is to understand the problem and translate it into an effective visualization design. In the latter case, a visualization designer has an idea for a new visual encoding, an interaction idiom, or a new algorithm. Sometimes, such ideas emerges during problem-driven visualization design.

## The Process of Visualizing Data

When preparing a data visualization project, we are often wondering where to begin with in the first place? From data collection, cleaning, exploration, analysis and visualization, there is a lot that needs to be done in order to derive an insight from data. As you can imagine, there are many proposed data visualization pipelines (e.g., {cite}`fry2008visualizing`, {cite}`kirk2019data`). However, I would like to focus on one proposition - the four levels nested model of visualization design {cite}`munzner2014visualization`. Munzner proposed to divide the problem of visualization design into four cascading levels: (1) the situation level, which contains details of a specific application domain; (2) the data/task abstraction level, where the domain-specific problems and data are separated from context; (3) the visual encoding/interaction idiom level, where the data are visualized and interaction is added; (4) the algorithmic level, where the algorithm is realized to computationally instantiate these idioms. These levels are nested, which means that if you make a bad choice in the abstraction phase, then even perfect choices at the idiom and algorithm levels will not result in a visualization solution that solves the intended problem. For example, you misunderstand the context, and thus, the needs of your stakeholders, because of that you are focusing on the wrong data that are being visualized with a insufficient idiom. Finally, it could happen that your code is too slow. Visualization design is usually a highly iterative refinement process, in other words, visualization design follows the principle of design as redesign. In the following, I detail each of these levels.

The question arises, how you can tackle these challenges properly. Munzner proposes here an immediate validation and downstream validation, in other words, she recommends to properly reflect on each stage on your design decisions before your enter the next level. Taking this very validation-centered perspective on vis design and if you consider that the design of visualizations follows the principle of design as redesign, then your see the parallels to the human-centered design process. You can easily map the Munzner's levels on the HCD process, which makes it easier to position all the methods you already know in Munzner's model.

### The situation level

The __Domain Situation__ contains the details of a specific application domain. This level focuses on a specific domain situation, which encompasses a group of target users, their domain of interest, their questions, and their data. A domain relates to a particular field of interest of the target users of a vis tool, for example open access, microbiology, or health care. Each domain usually has its own vocabulary for describing its data and problems, and there is usually some existing workflow of how the data is used to solve their problems. A group of target users can be narrowly defined as a handful of people working at a specific company, or broadly defined as anybody who does research. 

__Domain Validation__ Primary threat is the mischaracterizing of the the problem
An immediate form of validation is to interview and observe the target audience to verify the characterization. Contextual inquiry is typically better suited for vis designers than silent observation because of the complex cognitive tasks that are targeted.
One downstream form of validation is to report the rate at which the tool has been adopted by the target audience. A tool that is actually used by its intended users has reached a different level of success than one that has only been used by its designers.

### The data/task abstraction level

The __Data/Task Abstraction__ (What-why-level) separates the domain-specific problems and data from the context.
Your goal is to determine which data type would support a visual representation that addresses the user’s problem.
Abstracting specific domain questions and data into a domain-independent vocabulary. It allows you to identify situations that are similar, even though there are using a very different language.
Questions from very different domain situations can map to the same abstract vis tasks. We talked about abstract tasks such as browsing, comparing, and summarizing.  The data abstraction level requires you to consider whether and how the same dataset provided by a user should be transformed into another form.

__Abstraction Validation__
The main thread is that the identified task and designed data abstraction do not solve the characterized problems. 
A immediate validation is that the system must be tested by target users, rather than doing an abstract task specified by the vis system developers.
A common downstream form of validation is to have a member of the target user community try the tool in controlled user studies. A more rigorous validation approach for this level is to conduct a field study.
Other evaluation methods for visualizations focus on data insight (types of insight visualizations provide and the time it takes to acquire it). 

### The visual encoding/interaction idiom level

The __Visual Encoding/Interaction Idiom__ maps the data and task on a visual coding and adds interaction capabilities. 
Decision on a specific way to create and manipulate the visual representation of the abstract data, guided by the abstract tasks that you also identified.  There are two major concerns at play with idiom design: (1) How to create a single picture of the data? It defines the visual encoding idiom controls exactly what users see. (2) How to manipulate that representation dynamically? The interaction idiom controls how users change what they see. 

__Idiom Validation__
Threat is that the chosen idioms are not effective at communicating the desired abstraction to the person using the system. 
One immediate validation approach is to justify the design of the idiom with respect to known perceptual and cognitive principles by using heuristic evaluation or expert reviews. Downstream validation approaches are
* a controlled experiment in a laboratory setting: Evaluating the impact of specific idiom design choices by measuring human performance on abstract tasks or getting qualitative feedback;
* presentation of and qualitative discussion of results in the form of still images or videos as usage scenarios; and
* quantitative measurement of result images (e.g., number of edge crossings in networks.

### The algorithmic level

The __Algorithm__ translates the idioms in a concrete programming language. The level involves all of the design choices involved in creating an algorithm. The goal is to efficiently handle the visual encoding and interaction idioms. The nested model emphasizes separating algorithm design, where your primary concerns are about computational issues, from idiom design, where your primary concerns are about human perceptual issues. There is an interplay between these levels. For example, a design that requires something to change dynamically when the user moves the mouse may not be feasible if computing that would take minutes or hours instead of a fraction of a second.

__Algorithm Validation__ The primary threat is that the algorithm is suboptimal in terms of time or memory performance, either to a theoretical minimum or in comparison with previously proposed algorithms. 
An immediate form of validation is to analyze the computational complexity of the algorithm.
The downstream forms of validation:
* Measure the wall-clock time and memory performance of the implemented algorithm
* Determine what data you should use to test the algorithm (use benchmarks)
* Verify the correctness of the algorithm whether through careful testing or formal methods.

### Validity of Your Vis Design

We differentiate three types of validity: construct validity, internal validity, and external validity.

For example, if a hypothesis states that ''self-esteem'' increases with age, research tracking self-esteem over time from social media must ask whether its assessment of self-esteem from text is actually measuring ''self-esteem'' versus other related or unrelated constructs. In other words, are the observed behaviors (such as words used or frequency of posting) driven primarily by self-esteem as opposed to community norms, variations in system functionality, or other individual aspects. 

Internal validity or does our analysis correctly lead from the measurements to the conclusions of the study? For example, an analysis of whether self-esteem increases with age may not be internally valid if data cleaning accidentally removes messages expressing confidence; or if machine learned classifiers were inadvertently trained to recognize self-esteem only in younger people. Of course, while we do not dwell on them, researchers should also be aware of more blatant logical errors—e.g., comparing the self-esteem of today’s younger population to the self-esteem of today’s older population would be consistent with but would not actually prove that self-esteem increases with age. 

For example, effects observed on one social media platform may manifest differently on another platform due to platform differences, differing community or cultural norms. This concept includes what is sometimes called ecological validity, which captures the extent to which an artificial situation (constrained social media platform) properly reflect a broader real-world phenomenon. For example, even after we conclude a successful study of self-esteem in a longitudinal social media dataset, its findings may not generalize to a broader setting because of worries that the kinds of people who self-select into a particular platform are not representative of the broader setting; or that the behaviors they express online may not be representative of their behaviors in other settings.

Each type of Validity has a tradeoff depending on the method applied (see {numref}`tradeoff-fig`).

```{figure} ./images/tradeoff_validity.png
---
width: 100%
name: tradeoff-fig
align: center
---
Types of Validity and Tradeoff. Taken from (Padilla, 2018)
```

## Mapping the Human-Centered Design Process and the Nested Model

In {numref}`01-hcdv`, we introduced the human-centered design process; how can we bring the nested model and the human-centered design approach together? We can map the analysis step onto the domain situation level, the idea/concept step onto the data/task abstraction level, the design prototype step onto visual encoding/interaction idiom level and the algorithmic level. What is the advantage of this mapping? We can apply all methods, we know from human-centered design for designing our visualizations. 

In her visualization design work, Munzner realized that different ways to get a visualization design wrong {cite}`munzner2014visualization`. You might identify the wrong problem, by misunderstanding user's needs. You might focus on the wrong data and tasks, thus, you're showing them the wrong thing. You might decide for the wrong idiom, thus, the way you show the data doesn't work. Finally, you might implement the visualization correctly, thus your code is too slow.

## Major Elements of Visualization Design

In the following, we want to focus on the major elements of visualization design the what–why–how questions which translate into a data–task–idiom trio. By focusing on this trio, we need to answer the following questions:
* What data is shown in the views?
* Why is the task being performed?
* How is the vis idiom constructed in terms of design choices?

In the following, we look into each question in more detail.

### Reflecting on Data

Back in 2017, the newspaper ''The Economist'' published a story titled, "The world's most valuable resource is no longer oil, but data." Since its publication, the topic has generated a great deal of discussion, and "Data is the new oil" has become a common refrain. How could this happen? 

Already in 2008, the Wired magazine editor Chris Anderson titled in an article "The End of Theory," (https://www.wired.com/2008/06/pb-theory/). 

> This is a world where massive amounts of data and applied mathematics replace every other tool that might be brought to bear. Out with 
> every theory of human behavior, from linguistics to sociology. […] Who knows why people do what they do? The point is they do it, and we > can track and measure it with unprecedented fidelity. With enough data, the numbers speak for themselves.
>
> --- Chris Anderson, WIRED, 2008

Anderson made the claim that “with enough data, the numbers speak for themselves.” The article explains several examples of how the abundance of data helps people and companies take decision without even having to understand the meaning of the data itself. His assertion was that the age of Big Data will soon permit data scientists to do analysis at the scale of the population. Statistics is based on the idea that you can infer things about a population by taking a random and representative sample.At the point when we have data collected about an entire population, theory is no longer necessary. We also, he wrote, don't need models and theories to understand why something is happening, just to be able to see that one thing is correlated with another: “Correlation is enough.”

As D'Ignazio and Klein {cite}`dignazio2020datafeminism` point out, there is a misconception when saying that “numbers speak for themselves”. The assumption is that data are a raw input rather than seeing them as artifacts that have emerged “fully cooked” into the world, birthed out of a complex set of social and political circumstances already existing in the data setting. But data is an output first. After that, it can become an input into a new process, but only with understanding of what the limitations of the collection environment were. “Raw Data” is an Oxymoron. Many data-driven projects aiming towards producing new, future insights forget to interrogate how the data got collected and cooked in the first place.

What is the difference between data, information, and knowledge?

The following three points summarize the essential differences between the three concepts {cite}`aamodt1995datainformationknowledge`:
Data are syntactic entities, i.e., data are patterns with no meaning; they are input to an interpretation process, i.e.
to the initial step of decision making. Information is interpreted data, i.e., information is data with meaning; it is the output from data interpretation as well as the input to, and output from, the knowledge-based process of decision making. Knowledge is learned information, i.e., knowledge is information incorporated in an agent's reasoning resources, and made ready for active use within a decision process; it is the output of a learning process. The role of knowledge, in general, is therefore to play the active part in the processes of transforming data into information, deriving other information, and acquiring new knowledge, i.e., to learn. This leads to the following summary of knowledge roles: knowledge is needed to transform data into information; knowledge is needed to derive new information from existing; knowledge is needed to acquire new knowledge, thus is referred to as data interpretation, to as elaboration, and to as learning.

<!-- A distinction between data and information is that data are uninterpreted characters, signals, patterns, signs, i.e. they have no meaning for the system concerned. Data becomes information after having been interpreted to give meaning. This is illustrated in the figure by the Data Interpretation arrow. In order to interpret data into information, a system needs knowledge.-->

<!-- Once the data has been given an interpretation as information (an initial interpretation, at least) by the process described above, it is elaborated upon in order to be better understood and for deriving (inferring) new information. This is illustrated by the Elaboration arrow. Information that may be inferred in this way includes additional problem features, generated hypotheses, consequences of hypotheses, suggested solutions to problems, explanations and justifications of suggestions, critiquing arguments, etc. The elaboration process is the actual problem solving process, i.e. where the core decision-making takes place. Interpretation of data into information may be viewed, simplified, as a kind of pre-processing with respect to the core of the decision making process. However, frequent interaction with the environment during decision making blurs this picture and illustrates the over-simplification of such a view. In a more realistic decision-making process, elaboration and data interpretation are interleaved; initial interpretations get modified during elaboration, elaboration leads to questioning of the environment, which in turn leads to new or revised data being entered, or to revised interpretations of previous data.-->

<!-- A system's knowledge grows and gets modified through interaction with the environment. This process is what we call learning. A widely shared view is that learning is the integration of new information into an existing body of knowledge, in a way that makes it potentially useful for later decision making. New knowledge may also come from inference processes within the knowledge body itself. This is illustrated by the two Learning arrows in the figure, respectively. We here focus on learning as the process that produces knowledge, this also says something important about what knowledge is. -->

As Donna Harraway emphazised all knowledge is “situated.” {cite}`haraway1988situated` It means that context matters.  When we want to create new knowledge based on a given dataset, we have to reflect about the social, cultural, historical and material conditions in which that data was produced, as well as the people who created that data.Rather defining data as objective, that can be taken as it is, we need to connect data back to their context, to better understand existing limitations, but also for example, ethical obligations, or existing privacy concerns. However, we also need to think about our own role when analyzing the data. What is our perspective we bring in and how we decide which part of the data are valuable and which don’t. To come back to Chris Anderson. His post was possible also a provocation but when working with data, we need *more* theory, context, and scientific methods, not less. Why? Because data is often created by humans or by software that was designed by humans. Thus, it makes sense to add qualitative data to a dataset.

Thick Data or qualitative data is data brought to light using qualitative, ethnographic research methods that uncover people’s emotions, stories, and models of their world {cite}`wang2016bigdata`. It’s the sticky stuff that’s difficult to quantify. It comes to us in the form of a small sample size and in return we get an incredible depth of meanings and stories. Thick Data is the opposite of Big Data (or thin data), which is quantitative data at a large scale that involves new technologies around capturing, storing, and analyzing. For Big Data to be analyzable, it must use normalizing, standardizing, defining, clustering, all processes that strips the the data set of context, meaning, and stories. Thick Data can rescue Big Data from the context-loss that comes with the processes of making it usable.

Big Data requires a humongous N to uncover patterns at a large scale while Thick Data requires a small N to see human-centered patterns in depth. Both types of Thick Data relies on human learning, while Big Data relies on machine learning. Thick Data reveals the social context of connections between data points while Big Data reveals insights with a particular range of quantified data points. Thick Data techniques accepts irreducible complexity, while Big Data techniques isolates variables to identify patterns. Thick Data loses scale while Big Data loses resolution.

Thus it makes sense to take a human-centered design approach. You should think about the audience, the purpose and the context of your research. 
* Audience: Who are you publishing your research for?
* Purpose: How do you want them to use your research?
* Context: What factors (under your control) will impact whether/how they use it? 

Publishing your research openly shows that you take responsibility for your research. Including the possibility that you might be wrong. It provides transparency around your values, motivations, and assumptions. Having a public audience in mind when designing and publishing your projects encourages you to reflect on your values, motivations, assumptions, and thought process—and how that might influence your project. Thinking in terms of HCD can also help you think of trade-offs in open research. For example, it can help you decide when/what NOT to publish openly! 

#### Data Set

What kind of data are you given? What information can you figure out from the data, versus the meanings that you must be told explicitly? What high-level concepts will allow you to split datasets apart into general and useful pieces? To move beyond guesses, you need to know two crosscutting pieces of information about these terms: their semantics and their types. The semantics of the data is its real-world meaning. 

A dataset is any collection of data. There are four basic dataset types: tables, networks/trees, spatial (fields, geometry). In real-world situations, complex combinations of these basic types are common. 

Consider the concept of a table as a type of record that is independent of any particular visual representation. In (simple flat) tables, each row represents an item of data, and each column is an attribute of the dataset. Each cell in the table is fully specified by the combination of a row and a column and contains a value for that pair. A multidimensional table has a more complex structure since each cell is indexed by multiple keys. It can be a table in a table, which is called a tensor. 

Networks are well suited for specifying some kind of relationship between two or more items. An item in a network is often called a node (or vertex). A link (or edge) is a relation between two items. Nodes can have associated attributes, just like items in a table.Links could also have attributes associated with them; these may be partly or wholly disjoint from the node attributes. Networks can also be represented by two tables. Networks with hierarchical structure are more specifically called trees. In contrast to a general network, trees do not have cycles: each child node has only one parent node pointing to it. 

The field dataset type also contains attribute values associated with cells. Each cell in a field contains measurements or calculations from a continuous domain. Continuous phenomena include temperature, pressure, speed, force, and density (or mathematical functions).
Continuous data requires careful treatment that takes into account the mathematical questions of sampling, how frequently to take the measurements, and interpolation, how to show values in between the sampled points in a way that does not mislead.

The geometry dataset type specifies information about the shape of items with explicit spatial positions. The items could be points, or one-dimensional lines or curves, or 2D surfaces or regions, or 3D volumes. Spatial data often includes hierarchical structure at multiple scales. 

#### What Data Types Should be Differentiated?

An attribute is some specific property that can be measured, observed, or logged. For example, attributes could be salary, price, or protein expression levels. 
An item is an individual entity that is discrete, such as a row in a simple table. For example, items may be people, stocks, or genes.
A link is a relationship between items, typically within a network.  
A position is spatial data, providing a location in two-dimensional (2D) or three-dimensional (3D) space.
A grid specifies the strategy for sampling continuous data in terms of both geometric and topological relationships between its cells. 

(variabletype)=
#### What Attribute Types Do you Know? 

What kind of data are you given? What information can you figure out from the data, versus the meanings that you must be told explicitly? What high-level concepts will allow you to split datasets apart into general and useful pieces?

To move beyond guesses, you need to know two crosscutting pieces of information about these terms: their semantics and their types. The semantics of the data is its real-world meaning. 

```{figure} ./images/attribute_types.png
---
width: 100%
name: attribute_types-fig
align: center
---
Types of variables encountered in typical data visualization scenarios. Taken from (https://clauswilke.com/dataviz/aesthetic-mapping.html)
```

### Reflecting on Tasks

Why Analyze Tasks Abstractly? You need to consider tasks in an abstract form, rather than the domain-specific way that users typically think about them. Transforming task descriptions from domain-specific language into abstract form allows you to reason about similarities and differences between them. 

Munzner {cite}`munzner2014visualization` differentiated a small set of carefully chosen words to describe why people are using visualization, designed to help you crisply and concisely distinguish between different goals. We differentiate a set has verbs describing actions, and nouns describing targets.

#### User Goals are Defined by Actions 
We can define three levels of action. The high-level choices describe how the visualisation is being used to analyze, either to consume existing data or to also produce additional data. The mid-level choices cover what kind of search is involved, in terms of whether the target and location are known or not. The low-level choices pertain to the kind of query: does the user need to identify one target, compare some targets, or summarize all of the targets? Decisions at each of these three levels are independent, and it is usually useful to describe actions at all three levels.

_Action: Analyze for Consumption or Production_ In contrast to the use of vis only for the consumption of existing information, in the production case the intention of the user is to generate new material. Often, the goal in production is to produce output that is immediately used as input for a next instance. Sometimes the user intends to use this new material for some other vision-related task, such as discovery or presentation. Sometimes the intended use of the new material is for another purpose that does not require a vis, such as downstream analysis with non-visual tools. There are three types of production goals: Annotate, Record, and Derive.

_Action: Search and their Classification_ All high-level analysis cases require the user to search for items of interest within the vis as a middle-level target. The classification of search into four alternatives is broken down according to whether the identity and location of the search target is already known or not. If users already know both what they’re looking for and where it is, then the search type is simply lookup.  If users want to find a known target at an unknown location, the search type is locate, that is, find out where the specific object is. If users don’t know exactly what they’re looking for, but they do have a location in mind of where to look for it, the search type is browse. If users are not even sure of the location, the search type is explore.

_Action: Query_
A low-level user goal is to query targets at one of three scopes. Once a target or set of targets for a search has been found, a low- level user goal is to query these targets at one of three scopes: identify, compare, or summarize. The progression of these three corresponds to an increase in the amount of search targets under consideration: one, some, or all. That is, identify refers to a single target, compare refers to multiple targets, and summarize refers to the full set of possible targets.

_Actions Refer to Targets_
All actions refer to a target, i.e. an aspect of the data that is of interest to the user. The idea of a goal is explicit in search and query actions. It is more implicitly related to the usage actions, but still relevant: for example, what the user presents or discovers.

Tasks are defined by a {action, target} pairs, for example, discover distribution, compare trends, locate outliers, browse topology. 

### The How of Visualization Design - At A Glance

Bostock et al. {cite}`Heer_Bostock_Ogievetsky_2010` state: 

> All visualizations share a common “DNA” – a set of mappings between data properties and visual attributes 
> such as position, size, shape, and color – and customized species of visualizations might always be constructed > by varying these encodings.


__More Coming Soon__


<!-- ## The What-Why-How of Visualization Design
The design space of possible visualisation idioms is huge, and includes the considerations of both how to create and how to interact with visual representations.
Visualization design is full of trade-offs, and most possibilities in the design space are ineffective for a particular task, so validating the effectiveness of a design is both necessary and difficult. You must take into account three very different kinds of resource limitations: those of computers, of humans, and of displays. 
Visualisation usage can be analysed in terms of why the user needs it, what data is shown, and how the idiom is designed. 

### Knowledge the Design Space of Possible Visualizations
First, there is the space for all possible solutions, including possible solutions that no one has ever thought of. 
Next, there is the set of possibilities known to you, the vis designer. Of course, this set might be small if you are a beginner who is not familiar with the full range of methods that have been proposed in the past. If you are in this situation, one of the goals of this event is to expand the set of methods. 

The next set is the consideration space, which contains the solutions you are actively considering. This set is necessarily smaller than the known space, since you cannot consider what you do not know. An even smaller set is the proposal space of possibilities that you explore in detail via prototyping. Eventually, one of them becomes the chosen solution.

Is it a good solution? Probably not.



We have learned last week that we live a data area. However, data are not meaningful by themselves. We need to find appropriate approaches to explore data, to relate data to each other, and to communicate it meaningfully~\cite{KlingStar1998:HCD}.

## Übung
https://docs.google.com/document/d/1HDAyT5tCVR0uRmt4FpkjNsGlA1fKBMiWES87dVDEjjE/edit#heading=h.jmyr3335vjfs
http://www.cond.org/vizitcards.pdf
https://pdritsos.com/files/Roberts-et-al-FDS-2016.pdf

## Data
* data sheets

## Side Topic: Meaning

Understanding is the ability to grasp the meaning of information. Information is conveyed in a message using a specific language. Information is understood by the receiver of a message, if the receiver interprets the information correctly. A correct interpretation depends on Syntax, Semantics, and Pragmatics.

### Syntax
* It originates from the greek language and means arrangement and ordering.
* In grammatics syntax denotes the study of principles and processes by which sentences are constructed in particular languages.
* In formal languages, syntax is just a set of rules, by which well formed expressions can be created from a fundamental set of symbols (alphabet).
* In computer science, syntax defines the normative structure of data.

### Semantics
* It originates from the greek language. It pertains to the character, the study of meaning.
* Is part of the linguistics focussed on Sense and Meaning of language or symbols of language.
* Is the study of interpretation of signs or symbols as used by agents or communities within particular circumstances and contexts.
* Semantics asks, how sense and meaning of complex concepts can be derived from simple concepts based on the rules of syntax.
* The semantics of a message depends on context and pragmatics.

### Pragmatics
* It originates from the greek language and relates to action.
* It reflects the intention by which the language is used to communicate a message.
* In linguistics, pragmatics denotes the study of applying language in different situations.
* It also denotes the intended purpose of the speaker.
* Pragmatics studies the ways in which context contributes to meaning.

### Example Traffic Light Situation
* (Awareness) Syntax: green (bottom); yellow; red
* Semantic: green = go; …; red = stop
* Pragmatics: If red and no traffic then it is allowed to go

### Difference between Data Type and Semantics
* The data type is an abstract classification that has implications on 
mathematical operations data structure (how the data are stored, e.g. boolean, short, int, float, double, string)
* The abstract type provides a description of the data. It is characterized by methods / attributes and it may be organized into a hierarchy.
* Remember, if the semantics is given, the type will follow.


## Data Needs Context

https://medium.com/big-data-small-meaning-and-global-discourses/research-data-is-a-product-of-its-time-67e972aea9b7
https://raley.english.ucsb.edu/wp-content/Engl800/RawData-excerpts.pdf
https://data-feminism.mitpress.mit.edu/pub/czq9dfs5/release/3
https://medium.com/@kanarinka/what-would-feminist-data-visualization-look-like-aa3f8fc7f96c
https://medium.com/nightingale/the-data-are-not-objective-and-neither-are-you-285b15a1b584
https://library.oapen.org/bitstream/handle/20.500.12657/22273/9789048543137.pdf?sequence=1%20#page=392
https://transmarcations.constantvzw.org/texts/Pierre_Visions_carto.pdf






Here you can see what happens if you consider a larger space of possible solutions.

A basic design principle is to consider multiple alternatives and then choose the best one, rather than immediately focusing on one solution without considering alternatives. One way to ensure that more than one possibility is considered is to explicitly generate multiple ideas in parallel.

In the following, I will introduce a framework that helps you to get structure on the huge design space. Such scaffold will help you to think systematically about choices.




## Validity
https://medium.com/multiple-views-visualization-research-explained/how-do-we-know-when-a-visualization-is-good-c894b5194b62
Padilla, L. M. (2018, October). A case for cognitive models in visualization research: Position paper. In 2018 IEEE Evaluation and Beyond-Methodological Approaches for Visualization (BELIV) (pp. 69-77). IEEE.


