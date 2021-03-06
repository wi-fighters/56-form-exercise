# Accessible responsive form

In this example, we'll create a form that a customer can use to update their delivery and billing addresses.

Here are the mockups of how it'll look:

![Mockup of mobile version](./mobile.png)
![Mockup of desktop version](./desktop.png)

Keep a browser window open alongside your code as you go.

## Part 1: Form structure

1. Create an appropriate-level heading to describe your form. Call it `Update Addresses`.

2. Create a `form` element. Give it an `action` attribute with a value of `#`.

3. Create an `input` element. Give it a `type` attribute with the value `submit`, and a `value` attribute with the value `Update Address Details`. This element should stay at the end of the form.

## Part 2: Delivery address

### Text inputs

1. Create an `input` element. Give it the following attributes:
    - `type` attribute with the value `text`
    - `id` attribute with the value `first` (`id` will be used by the `for` attribute of the `label` element in the next step)
    - `name` attribute with the value `first` (`name` will be used by the form-handling script to grab the data from this field)
    - `placeholder` attribute with the value `Kenny`

2. Create a label element and wrap it around the above input. Give it a `for` attribute with the value `first` (this should match the above `id` of the element being labeled). Follow this format exactly:

```html
<label for="first">First name
    <input type="text" id="first" name="first" placeholder="Maggie">
</label>
```

3. To make the last name field, copy the above (label and input). Update the following:
    - on the `input` element:
        - `id` value becomes `last`
        - `name` value becomes `last`
        - `placeholder` value becomes `Simpson`
    - on the `label` element:
        - `for` becomes `last` (to match the `id` we just changed)
        - Label text becomes `Last name` (after the label's opening tag)

4. To make the company field, copy the above (label and input). Update the following:
    - on the `input` element:
        - `id` value becomes `company`
        - `name` value becomes `company`
        - `placeholder` value becomes `The Simpsons`
    - on the `label` element:
        - `for` becomes `company` (to match the `id` we just changed)
        - Label text becomes `Company` (after the label's opening tag)

5. Copy the pattern above to create form fields for `street` `number`, `city` and `postcode`. For placeholders, you can use `Evergreen Terrace`, `742`, `Springfield` and `58008` respectively.

### Providing multiple options

Both ways are worth knowing. They each have their pros and cons.

#### Alternative 1: Using a text input with a datalist

Pros: Allows typing for improved UX.
Cons: Support is limited. No grouping possible yet

6. Using the same pattern as above, create a text input wrapped in a label. Change the following:

    - on the `input` element:
        - `id` value becomes `state`
        - `name` value becomes `state`
        - `placeholder` value becomes `Oregon`
        - add a new attribute `list` with a value of `states` (this will match the `id` of our datalist)
    - on the `label` element:
        - `for` becomes `state` (to match the `id` we just changed)
        - Label text becomes `State&nbsp;/&nbsp;Region` (after the label's opening tag)

7. Add a `datalist` element with an `id` of `states` (should match the `list` attribute of your `input` element above)

Nested between the `datalist` tags, define the following `option` elements:

- `California` (value of `CA`)
- `Colorado` (value of `CO`)
- `Louisiana` (value of `LA`)
- `New York` (value of `NY`)
- `Oregon` (value of `OR`)
- `Texas` (value of `TX`)

Follow this format for all options:

```html
<option value="CA">California</option>
<option value="CO">Colorado</option>
```

#### Alternative 2: Using a select element

Pros: Widely supported, allows grouping.
Cons: Poor UX when typing.

8. Create a `select` element with an `id` of `country`.

9. Wrap your `select` element with a `label`. The label's `for` attribute should be `country` (to match the `id` of the `select` element). Inside the opening label tag, the label's text should be `Country`.

So far it should look like this:

```html
<label for="country">Country
    <select id="country">
    </select>
</label>
```

10. Inside the `select` element, create three empty `optgroup` elements. Give each of them a `label` attribute, with the values `Asia`, `Europe` and `North America`.

Nested between the corresponding `optgroup` tags, define the following `option` elements:

- `Thailand` (value of `TH`)
- `Japan` (value of `JP`)
- `France` (value of `FR`)
- `Germany` (value of `DE`)
- `Canada` (value of `CA`)
- `United States` (value of `US`)

11. To provide an empty default option, create a new `optgroup` with a label attribute of `None`. We don't want the user to be able to select it, so add the empty attribute `disabled`.

12. Inside this new `optgroup` add an `option` with the text `-- choose one --` and set the `value` attribute to `default`. Also set the following empty attributes to the `option`: `selected`, `disabled` and `hidden`.

## Part 3: Billing address

We're going to separate both addresses with `fieldset` elements, so the first steps to adding the billing address will be to prepare the delivery address.

1. Wrap all the above elements in a `fieldset` element (except the submit button). Nest a `legend` element as the first child of your new `fieldset`, and give it the text `Delivery Address`. The result should look like this:

```html
<form action="#">
    <fieldset>
        <legend>Delivery Address</legend>
        <!-- your form fields here -->
    </fieldset>
</form>
```

2. Add a second fieldset in the same form. This time give it a `legend` of `Billing Address`.

3. Copy in the fields from the previous example. **Use your judgment to decide** what you will need to change in your existing code so that your `id` and `name` attributes remain unique. E.g. `deliveryStreet` and `billingStreet`. Do this for all applicable fields.

4. Consider, what could you do to make your `datalist` implementation more DRY?

## Part 4: Responsive styling

### Big-picture layout

1. On big screens, we'll want the form to be contained to one center column. For this we'll need a container around the `form` and its `heading`. Make this a `div` with a class of `form-container`.

**When adding containers, remember to carefully adjust your indentation**

2. Give your `.form-container` a `max-width` of `40rem` and apply a `margin` that will automatically center it horizontally.

3. Create some more containers (and adjust indentation) for the elements that we want to appear inline. Add a `div` with the class `inline-container` around the following pairs of elements (in both fieldsets):

- first + last name
- street + number
- city + postcode
- state + country

4. Link to [normalize.css](https://necolas.github.io/normalize.css/8.0.1/normalize.css) and also start your own style sheet by giving all elements a `box-sizing` value of `border-box`.

5. With one ruleset (one pair of curly braces), target the `input` and `select` elements and give them a `width` of `100%`.

6. Make every `.inline-container` a flex container. **Use one shorthand property** to define a `flex-direction` of `row` and a `flex-wrap` of `wrap`.

7. Choose a selector that targets **all descendants of your flex containers** and apply the following styles:

- Set `flex-grow` to equally distribtue available space.
- Set `flex-shrink` to `0`.
- Indicate when to start wrapping by defining a `flex-basis` of `15rem`.
- Experiment with each of these to understand how they affect the layout. Then when you're ready, condense them into **one shorthand property** instead of three.

### Stylistic details

8. Improve UX by giving feedback to users when they interact with the `submit` button. Target it using an **attribute selector** and apply the following styles:

```css
/* all states */
cursor: pointer;
transition: 0.2s ease-out;

/* hover state */
transform: scaleX(1.03) scaleY(1.1);

/* active state */
background-color: #dfd1a7;
```

9. Set the following styles on the big layout elements:

```css
html {
    font-family: Arial, sans-serif;
    background-color: #f9f5f0;
    color: #321313;
}

.form-container {
    /* add these properties to your existing ruleset */
    background-color: #f2ead3;
    border-radius: 1rem;
    padding: 1rem 2rem 3rem;
}
```

10. Add the following style to both fieldsets:

```css
fieldset {
    margin-bottom: 2rem;
    padding: 1rem;
    border: 1px dotted #321313;
    border-radius: 0.3rem;
}
```

11. Adjust the spacing around elements by adding the following label styles:

```css
label {
    display: block;
    margin-top: 0.6rem;
}

label:not(:last-of-type) {
    margin-right: 1ch;
}
```

12. Update your existing ruleset for `input` and `select` elements to remove all borders and set their height to `2rem`. Also set a `margin-top` of `0.3rem`.

13. To all `input` elements, apply a `border-radius` of `0.3rem` and a `padding` of `1ch`.

## Bonus

- How would you mark certain fields as required? Consider both the code and the visual cues.

- Notice how field sizes are no longer full-width when wrapped to a single-column. Find out what's causing it and wrap it in a media query so it's only enabled for larger devices.

- How would you improve this form for usability? For aesthetic?

## More forms

Use what you've learned to build other kinds of forms:

- login (research password fields and a checkbox to stay logged in)
- quiz game
- order details (e.g. pizza toppings, clothing color and size, etc.)
