# An informal overview of NLP usage with 3D and VR

As a first step into understanding how Natural Language Processing could be better used with 3D games inside a Virtual Reality environment, I considered it was necessary to scan over whatever was available already on this subject.

I found some interesting an even important results that I mentally organized by implementation goals. Here, I set in some possible order my findings in the hope that would be shortcut to anyone starting to get their interest in these world.

You may object that these are huge and heteromorphus disciplines to be talking so lightly of "organizing their interaction", that's true, so I'm not claiming to be exhaustive, but practical.

My main interest when scanning these papers is on how the gap between language and objects in space is close, or how things in a VR environment are refered 


1- Natural Language Processing in training simulation environments

Training simulations with VR would simplify the access to expensive tools or dangerous situations without losing the "immersive" experience needed to achieve a good trainig. Or so is the idea.

And on this field, there's a paper from 1997, Natural language processing in virtual training environments, presents a system that uses speech as input for a training that is "hands-busy and eyes-busy". It has speech to text and, for the processing of text, it poses a domain specific semantic grammar where the terminal symbols are expected chunks of text corresponding to verbs or specific name of elements. 

So, for the phrase "Where is the handle?" it would return something like ask(location(handle)). 

At the same time, the grammar changes with context, so meaning is constrained on, let's suppose, one or other scene of the training process.

This is an approach that could grow too fast if more grammars are needed, but it relies on the idea that not everything would be said in a given context (everything could be said though, of course). It is because of this "context switching and expectation" that the system has a way to solve anaphora. 

The interaction here is only based on question and answers, not far from almost every chatbot currently on a webpage and the VR has more to do with the environment where the trainig is being set, not really a joint experience.


2- Text to Scene

There's another set of applications where NLP and VR come toghether in a more entangled way, they receive the unambiguous name of Text to Scene. The Scene part refers to actual 3D scenes. These systems persue an intuitive principal expressed in the paper from 2017, "SceneSeer: 3D Scene Design with Natural Language": 

"Designing 3D scenes is currently a creative task that requires significant expertise and effort in using complex 3D design interfaces. This effortful design process starts in stark contrast to the easiness with which people can use language to describe real and imaginary environments."

Kind of like playing god creating things just by naming them: "Let there be a brown couch in the corner".

And a bit like the first "Hello, world" I made with Blender and Google's Speech Recognition API:

Video

(I could not pronounce 'sphere' in a distinguishable way apparently).

Along with this paper that presents SceneSeer, there's also one introducing WordsEye, from 2001, and another presenting AttribIT, from 2013.

For "WordsEye: An Automatic Text-to-Scene Conversion System", the authors use a series of steps from text to a semantic representation compatible with a database of 3D images. 

First, the texts gets parsed by a dependency parser, then semantic representations are derived from the dependency estructure using semantic interpretation frames. 
For nouns, they use WordNet to retrieve all possible hypernyms and hyponyms and match them with 3D objects in a database that are also tagged with this variations.
For verbs, they use argument structures to define the rol of the different elements returned from the parser. 

They also solve anaphora and correference based on morphological and semantic information of "the context" (whatever that means in this situation, words?, tags in the 3D objects?, previous sentences?). Anyway, from a linguistic side, the implementation is really interesting.

So, according to the paper, the semantic representation outputed by the linguistic analysis of the sentence "The cowboy rode the red bicycle to the store" would be:
1. Entity: cowboy
2. Entity: bicycle
3. Entity: store
4. Attribute:
    Subject: <element 2>

    Property: red
5. Action:
    Actor: <element 1>

    Action: ride
    Object: <element 2>

    Path: <element 6>
6. Path:
Relation: to
    Figure: <element 5>
    Ground: <element 3>
After this, the semantic elements need to be "depictable" by some "depiction rules" that describe a pose, a position and an orientation and the actors involved in it. There are some other rules related to common sense (let's say, non verbalized) constraints for the 3D objects. For example, if I want to generate a scene where there's a sandwich on a table, I'm not saying it, but I'm imagining a dish between the two objects, those kind of constraints.


In "AttribIt: Content Creation with Semantic Attributes", the authors say the system uses "employs a database of exemplar designs, assumed to be compatibly segmented and labeled.". This database of 3D designs seems to be the backbone of the text to scene solutions, but the key point of this particular system is precissely the understanding of attributes, or adjectives. So the user could not only ask for a "brown couch" to be set on the scene, but also for an "ugly" one.

For the learning of this attributes associated to elements in the database, they used human annotation. 



The real goal of this text, is to catch up with all I ignore before the NVIDIA GTC "Towards conversational AI based interactions in the Metaverse"