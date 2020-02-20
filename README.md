This lab sheet and all other materials can be found on GitHub here: https://github.com/QMUL-ECS735P/lab-week-5/

# OWL, Ontologies, and Protege
> **Session objectives:**
>   - Get familiar with Protege
>   - Visualise class hierarchies
>   - Build a simple ontology
    
## 1. Introduction
In this lab we'll be using Protege, a program for creating and exploring ontologies. The lab machines already have protege installed, to run it simply open a terminal session and type:

```
protege
```

and it will start up. If you want to use your own computer, you can download Protege here: http://protegewiki.stanford.edu/wiki/Install_Protege5

The Protege wiki and University of Manchester tutorials would be useful to keep on hand, refer to them both when you get stuck:
  - http://protegewiki.stanford.edu/wiki/Main_Page
  - http://owl.cs.manchester.ac.uk/publications/talks-and- tutorials/protg-owl-tutorial/
  
## 2. Examining OWL ontologies with Protege
You should have a `pizza.owl` file included in the lab materials; open Protege and then open this pizza ontology. You may also open Protege and use "Open from URL..." and paste in this URL: https://www.raw.githubusercontent.com/QMUL-ECS735P/lab-week-5/master/pizza.owl

Click the `Entities` tab and explore the class hierarchy. You should see something like this on the left pane:
![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/01-class-hierarchy.png)

Select a specific class, such as AmericanHot, what can we learn about it? 

![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/02-class-description.png)

Along with classes, we also have object properties. Navigate to the `Object properties` tab to see all the properties defined in this ontology.

![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/03-object-properties.png)

## 3. Visualising class hierarchies
Navigate to `Window -> Tabs -> OntoGraf` and then click the now visible `OntoGraf` tab. Start selecting some classes from the class hierarchy to place them into the OntoGraf display.

Along the top of the OntoGraf display are a number of options to change how the classes are laid out in the display. Below is an example of the "Vertical Directed" display. Experiment with a few different displays so you can see how the class hierarchy is ordered.

![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/04-ontograf.png)

## 4. Creating ontologies with Protege
Your task is to create an ontology that formalises the following statements:

1) No one who appreciates Beethoven fails to keep silent when Moonlight Sonata is being played.
2) Guinea pigs are ignorant of music.
3) No one who is ignorant of music ever keeps silent when Moonlight Sonata is being played.
4) Therefore, guinea pigs don't appreciate Beethoven.

Take a moment to understand each of these statements, then identifiy the classes and object properties we'll need to formalise these statements in an ontology.

---

Create a new ontology by navigating to `File -> New` (or pressting `Ctrl+N`) and navigate to the `Entities` tab like before. To get you started, create two new classes:
- `appreciates_beethoven`
- `guinea_pigs`
by clicking the `add subclass` button. 

![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/05-add-subclass.png)


We need to construct our ontology such we can prove `guinea_pigs` and `appreciates_beethoven` are **disjoint**.

![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/06-disjoint-with.png)

## 5. Using a reasoner in Protege
Protege can use several powerful OWL reasoners to determine whether our ontology is valid. Go to the `Reasoner` menu and select the HermiT reasoner if it is not already selected, then go back to the menu and start the reasoner.

We want to use the reasoner to prove that `guinea_pigs` and `appreciates_beethoven` are disjoint. To do this, create a new class `nobody` and define it as a `SubClass Of` both `guinea_pigs` and `appreciates_beethoven`.

Press `Ctrl+R` to re-run our reasoner, and then in the `Classes` tab click on the drop-down menu on the right and select "Inferred".

We should see our `nobody` class inferred as a subclass of the _bottom_ concept (that's `owl:Nothing`).

![](https://github.com/QMUL-ECS735P/lab-week-5/raw/master/07-inferred-classes.png)
