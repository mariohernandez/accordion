# Accordion

by [Mario Hernandez](https://mariohernandez.io)

A purely HTML & CSS Accordion using the `<details>` HTML element.

To build the accordion in Drupal you need the [Paragraphs](https://drupal.org/project/paragraphs) contrib module. However, you can use Custom Blocks but the instructions below only apply to Paragraphs.

## Included assets

* Basic CSS styles
* Paragraph module Twig template suggestions:
  * Full accordion wrapper: `paragraph--accordion.html.twig`.
  * Individual accordion items: `paragraph--accordion-item.html.twig`.
  * Paragraph wrapper field (optional): `field--paragraph--field-accordion-item.html.twig`.

## Drupal architecture

1. Install and enable the paragraphs module.
1. Create a paragraph type called Accordion items (`accordion_items`):
    1. Add a plain text field called Question (`field_question`)
    1. Add a text, long field called Answer (`field_answer`)
1. Create another paragraph type called Accordion (`accordion`):
    1. Add an Entity reference revisions field
    1. Configure the field so it uses **Paragraph** as the type of item to reference
    1. Set the _Allowed number of items_ to **Unlimited**
    1. For reference type, select **Accordion item**
1. Navigate to the **Manage form display** tab for the Accordion paragraph type
    1. Set the Accordion items field widget to **Paragraph (stable)**
    1. Customize the widget settings to your preference.
1. Switch to the **Manage display** tab
    1. Set the field format to **Rendered entity**
1. Select the content type where you wish to add the Accordion
    1. Click the **Manage fields** tab
    1. Add a new Entity reference revisions field to the content type (`accordion`)
    1. Repeat steps 3 & 4 except this time select the **Accordion** as the reference type.

## Files placement

**NOTE**: _The custom twig templates provided in this repo only work if the machine names used during the paragraphs site building portion match exactly the machine names used in the instructions above. If you used different machine names you will need to rename the teplates accordingly_.

1. In your custom theme's _Templates_ directory, place the twig templates included in this repo into their respective directory (i.e. `paragraphs/`, `field/`)
1. Place the `accordion.css` in the directory where Drupal finds the compiled CSS files.
1. If needed, create a new Drupal library (i.e. accordion):

    ```yaml
    accordion:
      css:
        component:
          dist/css/accordion.css: {}  # Confirm the file path
    ```

1. If the previous step was completed, attach the newly created library to `paragraph--accordion.html.twig`:

    ```twig
    {{ attach_library('your-theme/accordion') }}
    ```

## Adding an accordion

1. Create a new node of the type you added the accordion paragraph type to
1. Add as many accordion items as you wish
1. After saving the page you should see a fully-built accordion
1. The accordion should expand/collapse as expected

### Resources

* [Plain HTML/CSS version of Accordion](https://codepen.io/mariohernandez/pen/jErEPoj) (codepen).
* Blog post about [Native Accordions](https://mariohernandez.io/blog/native-accordions-let-html-do-the-heavy-lifting/).
