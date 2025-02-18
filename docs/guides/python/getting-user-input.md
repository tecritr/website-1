---
title: Getting user input
sidebar_label: Getting user input
---

Making interactive web apps with Flet is a breeze! It's not just limited to displaying data, but you can request an input from a user and respond to various events generated by page controls.

## Buttons

`Button` is the most essential input control which generates `click` event when pressed:

```python
btn = ft.ElevatedButton("Click me!")
page.add(btn)
```

<img src="/img/docs/getting-started/getting-user-input-elevated-button.png" className="screenshot-50" />

All events generated by controls on a web page are continuously sent back to your script, so how do you respond to a button click?

## Event handlers

Buttons with events in "Counter" app:

```python
import flet as ft

def main(page: ft.Page):
    page.title = "Flet counter example"
    page.vertical_alignment = ft.MainAxisAlignment.CENTER

    txt_number = ft.TextField(value="0", text_align="right", width=100)

    def minus_click(e):
        txt_number.value = str(int(txt_number.value) - 1)
        page.update()

    def plus_click(e):
        txt_number.value = str(int(txt_number.value) + 1)
        page.update()

    page.add(
        ft.Row(
            [
                ft.IconButton(ft.icons.REMOVE, on_click=minus_click),
                txt_number,
                ft.IconButton(ft.icons.ADD, on_click=plus_click),
            ],
            alignment=ft.MainAxisAlignment.CENTER,
        )
    )

ft.app(target=main)
```

<img src="/img/docs/getting-started/getting-user-input-event-handlers.png" className="screenshot-50" />

## Textbox

Flet provides a number of [controls](/docs/controls) for building forms: [TextField](/docs/controls/textfield), [Checkbox](/docs/controls/checkbox), [Dropdown](/docs/controls/dropdown), [ElevatedButton](/docs/controls/elevatedbutton).

Let's ask a user for a name:

```python
import flet as ft

def main(page):
    def btn_click(e):
        if not txt_name.value:
            txt_name.error_text = "Please enter your name"
            page.update()
        else:
            name = txt_name.value
            page.clean()
            page.add(ft.Text(f"Hello, {name}!"))

    txt_name = ft.TextField(label="Your name")

    page.add(txt_name, ft.ElevatedButton("Say hello!", on_click=btn_click))

ft.app(target=main)
```

<img src="/img/docs/getting-started/getting-user-input-textbox.png" className="screenshot-50" />

## Checkbox

The [Checkbox](/docs/controls/checkbox) control provides you with various properties and events emmiters for ease of use.

Let's create a one checkbox ToDo:

```python
import flet as ft


def main(page):
    def checkbox_changed(e):
        output_text.value = (
            f"You have learned how to ski :  {todo_check.value}."
        )
        page.update()

    output_text= ft.Text()
    todo_check = ft.Checkbox(label="ToDo: Learn how to use ski", value=False, on_change=checkbox_changed)
    page.add(todo_check, output_text)

ft.app(target=main)
```

<img src="/img/docs/getting-started/getting-user-input-checkbox.png" className="screenshot-50" />

## Dropdown

```python
import flet as ft


def main(page: ft.Page):
    def button_clicked(e):
        output_text.value = f"Dropdown value is:  {color_dropdown.value}"
        page.update()

    output_text = ft.Text()
    submit_btn = ft.ElevatedButton(text="Submit", on_click=button_clicked)
    color_dropdown = ft.Dropdown(
        width=100,
        options=[
            ft.dropdown.Option("Red"),
            ft.dropdown.Option("Green"),
            ft.dropdown.Option("Blue"),
        ],
    )
    page.add(color_dropdown, submit_btn, output_text)

ft.app(target=main)
```

<img src="/img/docs/getting-started/getting-user-input-dropdown.png" className="screenshot-50" />