# canopy/accessible-html

Type-enforced accessibility for Canopy HTML. A drop-in replacement for the `Html` module that makes common accessibility violations impossible at compile time.

## Features

- **Required alt text**: `img` requires a `String` alt text argument -- no way to omit it
- **Required labels**: `inputText` must be wrapped in `labelBefore`, `labelAfter`, or `labelHidden`
- **Typed ARIA roles**: A closed union type prevents typos and provides autocompletion
- **Non-interactive enforcement**: `div`, `p`, headings, etc. use `Attribute Never` to reject event handlers at compile time
- **Screen-reader utilities**: `Accessible.Style.invisible` for screen-reader-only content
- **Focus management**: Skip navigation links and focus trap configurations
- **Keyboard helpers**: Typed key bindings for Enter, Escape, Arrow keys, Tab, etc.

## Quick Start

```canopy
import Accessible as Html
import Accessible.Aria as Aria
import Accessible.Landmark as Landmark
import Html.Attributes exposing (id, src)
import Html.Events exposing (onClick, onInput)


view : Model -> Html.Html Msg
view model =
    Html.div []
        [ Html.h1 [] [ Html.text "My App" ]
        , Html.img "Company logo" [ src "logo.png" ]
        , Html.labelBefore []
            (Html.text "Email")
            (Html.inputText model.email [ onInput EmailChanged ])
        , Html.button [ onClick Submit ] [ Html.text "Submit" ]
        ]
```

## Modules

| Module | Description |
|--------|-------------|
| `Accessible` | Drop-in replacement for `Html` with accessibility enforcement |
| `Accessible.Aria` | All ARIA states and properties as typed attributes |
| `Accessible.Role` | All WAI-ARIA roles as a union type |
| `Accessible.Landmark` | Landmark role attributes (banner, navigation, main, etc.) |
| `Accessible.Live` | Live region attributes (polite, assertive, atomic, busy) |
| `Accessible.Key` | Keyboard event helpers (Enter, Escape, Arrow keys, Tab) |
| `Accessible.Focus` | Focus management (skip nav, focus trap, focusOn) |
| `Accessible.Style` | Screen-reader-only visibility helpers |

## Migration from Html

1. Change `import Html` to `import Accessible as Html`
2. Add alt text to images: `img [ src "photo.jpg" ] []` becomes `Html.img "Photo description" [ src "photo.jpg" ]`
3. Wrap inputs in labels: `input [ type_ "text" ] []` becomes `Html.labelBefore [] (Html.text "Name") (Html.inputText "" [])`
4. Move event handlers from non-interactive elements to buttons

## License

BSD-3-Clause
