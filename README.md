# The Stack

1. ## The problem

Flow elements require **space** (sometimes referred to as white space) to physically and conceptually separate them from the elements that come before and after them. This is **the purpose of the margin property.** 

*However, design systems conceive elements and components in isolation.*     
*At the time of conception, it is not settled whether there will be surrounding content or what the nature of that content will be.*     
*One element or component is likely to appear in different contexts, and the requirement for spacing will differ.*  

*We are in the habit of styling elements, or classes of elements, directly: we make style declarations belonging/pertenecientes to elements.*     
*Typically, this does not produce any issues, but **margin is really a property of the relationship between two proximate elements**.*     
The following code is therefore problematic:

```css 
p {  
   margin-bottom: 1.5rem;  
} 
``` 
Since **the declaration is not context sensitive, any correct application of the margin is a matter of luck**.   
If the paragraph is preceded /precedido by another element, the effect is desirable.   
But a :last-child paragraph produces a **redundant margin**.   
Inside a padded parent element, this redundant margin combines with the parent’s padding to produce double the intended space. 

2. ## The	solution

The trick is to **style the context, not the individual element(s)**.   
The Stack layout primitive **injects margin between elements via their common parent**:

```css   
.stack > * + * { 
   margin-block-start: 1.5rem;` 
}
``` 

Using the adjacent **sibling combinator (+)**, margin-block-start **is only applied where the element is preceded by another element:** no “left over” margin. 

The universal (or wildcard) selector (**\***) **ensures any and all elements are affected**. The key **\* \+ \*** construct is known as the [**owl**](https://alistapart.com/article/axiomatic-css-and-lobotomized-owls)
