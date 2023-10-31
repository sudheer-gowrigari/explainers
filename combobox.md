## NOTE: THIS DOCUMENT IS IN EARLY DRAFT AND UNDER HEAVY REVISION


## Combobox Explainer

Last Updated:


1. Background and scope of this document
2. Overview of Combo-box
3. Recommended anatomy for version 1
4. Introduction of the filter attribute
5. Introduction of the search attribute
6. Introduction of multiple attribute
7. Keyboard behavior
8. Other approaches considered
9. Open Questions
10. Research


### Background and scope of this document


#### Background

From the early days of the web, form controls have been pivotal in creating interactive and dynamic user experiences. Elements like `<input>`, `<button>`, and `<select>` were foundational, offering basic interactivity. As the web matured, so did the demands of web designers and developers. They sought more versatile and customizable controls to cater to a myriad of designs and functionalities.

The `<select>` element, for instance, while functional, lacks flexibility. It offers limited customization, which often leads developers to craft their own solutions. These custom implementations, while visually appealing, often come at the cost of performance, reliability, and most importantly, accessibility.

Recognizing these limitations, the [`<selectlist>`](https://open-ui.org/components/selectlist/) was introduced. This element builds on the foundation of the `<select>` but provides greater flexibility. The `<selectlist>` lets developers create a button-triggered dropdown with customizable appearance and behavior. Paired with `<listbox>`, and inclusive of `<option>` and `<optgroup>`, it offers a modern, adaptable, yet accessible web control.

Right now, many websites have their own type of **'combobox'**, but they're all a bit different. We often see a mix of `<input>` fields and `<datalist>` elements trying to do the job, but it's not quite perfect. By creating a standard **`<combobox>`**, we're aiming to simplify things. 

This proposal for `<combobox>` builds upon the strengths of `<selectlist>` and `<listbox>`. It aims to offer a control that is versatile for developers, intuitive for users, and, above all, accessible to all.

By standardizing such elements, we hope to bridge the gap between design demands and the need for performant, reliable, and accessible web controls. 


#### Scope of this document

This document aims to provide a complete view of combo-box utilisation across the web to inform a potential proposal within Open UI. The goal of this document is to propose a very basic anatomy to simplify the initial shipment of `<combobox>` (or some other name) in the web platform. It will heavily build upon `selectlist` but provide a better accessible and extensible solution than that of an `input` bound with `datalist`.


#### Out of scope of this document

This document will not be attempting some of the complex scenarios found across the web that leverage various ways in which to represent multi-selected options. Additionally, it does not intend to cover the addition of options that are not available in a `<listbox>`. It will not cover multi-select but will leverage the resolutions defined by `selectlist`.

A good analogy for what this document will result in looking like is the [Tabs research document.](https://open-ui.org/components/tabs.research.parts/)


### Recommended anatomy for version 1

```
<combobox>
   <input type=selectlist>
   <listbox>
	<option>One</option>
	<option>Two</option>
   </listbox>
</combobox>
```


**Pros:**



* Clear Semantics: The `<combobox>` element explicitly conveys its purpose.

**Cons:**



* Introducing new element, `<combobox>`


### Anatomy of `<combobox>`:

<img src="images/image24.png" alt="Anatomy of combobox" style="width:55%;">


1. `<combobox>`: The root container that encapsulates the entire `combobox` structure. It provides context for the interaction between the `input` and the `listbox`.
   1. Slots:
      1. input
      2. listbox

   2. Attributes:
      1. **multiple**: Allows multiple options to be selected.
      2. **search**: Indicates the combobox will actively fetch results based on user input.
      3. **filter**: Indicates the combobox will narrow down visible options based on user input.
2. `<input type=selectlist>`: This is where the user can type input or view the selected option. It acts as the trigger to display the listbox.
   1. Slots:
      1. **placeholder** (optional): To display hint text when the input is empty.
      2. **selectedoption** (optional): To display the currently selected option from the `listbox`. ???
3. `<listbox>`: This container holds the selectable options. It's hidden by default and is displayed when the `<input type=selectlist>` is activated.
   1. Slots:
      1. option
      2. optgroup (optional)
4. `<option>`: Represents an individual selectable item within the `listbox`.
5. `<optgroup>` (Optional): A container to group related options together.
   1. Slots:
      1. **legend**: To label the group.
      2. **option**: The options within this group.
6. `<legend>` (Optional, within `<optgroup>`): Provides a label or title for a group of options within the `listbox`.


#### Default Behavior

Just like a regular dropdown, the <combobox> doesn't need much to get started. Here's how you can set it up with the basics:


```
<combobox>
  <option>Option 1</option>
  <option>Option 2</option>
  <option>Option 3</option>
</combobox>
```


When you use it like this, the combobox creates the parts you need: an input to drop down the list, a place showing your selected option, and the `listbox` itself.


##### Combobox with selectedoption/optgroup


```
<combobox>
    <input type="selectlist" placeholder="Select or type an item...">
    <selectedoption></selectedoption>
    <listbox>
        <option>Apple</option>
        <option>Banana</option>
        <!-- Group of options with a legend -->
        <optgroup>
            <legend>Citrus Fruits</legend>
            <option>Orange</option>
            <option>Lemon</option>
        </optgroup>
        <!-- Another group of options with a legend -->
        <optgroup>
            <legend>Berries</legend>
            <option>Strawberry</option>
            <option>Blueberry</option>
        </optgroup>
    </listbox>
</combobox>
```



### Introduction of the `filter` attribute

The introduction of the `filter` _bool_ attribute revolutionizes the way users interact with combobox elements. By narrowing down visible options based on real-time input.


```
<combobox filter>
    <input type="selectlist" placeholder="Select fruit">
    <listbox>
        <option>Apple</option>
        <option>Apricot</option>
        <option>Banana</option>
        <!-- ... -->
    </listbox>
</combobox>
```

![freeform](https://github.com/sudheer-gowrigari/explainers/assets/11438997/e2f3f811-4783-4ce2-b343-3a5594b32841) E.g: Type 'A' to quickly filter to 'Apple' and 'Apricot'.
</center>


### Introduction of the `search` attribute

The introduction of the `search` attribute support search with



* pattern
* startswith 
* Contains
* ..

The current behavior of `<selectlist>` is the _startswith_ value


```
<combobox search>
    <input type="selectlist" placeholder="Select fruit">
    <listbox>
       <option>Apple</option>
        <option>Apricot</option>
        <option>Banana</option>
        <!-- ... -->
    </listbox>
</combobox>
```
![combo-search](https://github.com/sudheer-gowrigari/explainers/assets/11438997/c5132f5c-4d5b-484b-a147-f78fbf7c9cc4)



### Introduction of `multiple` attribute

TBD


### Keyboard Behavior

TBD : [https://www.w3.org/WAI/ARIA/apg/patterns/combobox/](https://www.w3.org/WAI/ARIA/apg/patterns/combobox/) 



## Research

To keep this doc focused on the initial recommended approach, we've separated the research for parts and examples into another document that can be [found here](combobox-research.md)

## Appendix
### Explored Anatomy Options for ``<combobox>``
#### Approach 1


```
<input type="text" list="browsers"  />
<datalist id="browsers">
	<option>firefox</option>
	<option>Chrome</option>
</datalist>
```


**Pros:**



* Native elements

**Cons:**



* You can't achieve multi-select with `<datalist>`:
* grouping options or adding icons next to options, the `<datalist>` approach falls short.
* Inconsistent Browser Support: While most modern browsers support `<datalist>`, the appearance and behavior can be inconsistent across different browsers.


#### Approach 2


```
<selectlist combobox>
  <input type=selectlist>
  <listbox>
	<option>One</option>
	<option>Two</option>
  </listbox>
</selectlist>
```


**Pros:**



* Leveraging the existing `<selectlist>`

**Cons:**



* Need to rely on an opt-in attribute(`combobox`) to modify the behavior of `<selectlist>`.
