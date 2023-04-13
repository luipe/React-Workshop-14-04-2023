## Components

- The _Components_ are the building blocks of each React-Application
- Components can have logic, and reuse other components
  - Either basic html components, your own components, or components from libraries
- For creating a page, first structure it into logical pieces and then create the components for the pieces

## Example

<img src="img/big_techday.png" style="width: 100%; box-shadow: none"/>

## Configuration via Properties

- Components are reusable
- In order for that to be useful, we often need to adapt the something in component
- This can be achieved via so-called "Properties", or short "Props"

Example:

```tsx
// component:
export function NavigationItem(props: { label: string; selected?: boolean }) {
  const label = props.label;

  if (props.selected) {
    return <div className="SelectedNavigationItem">{label}</div>;
  }
  return <div className="NavigationItem">{label}</div>;
}

// usage:
export function Navigation() {
  return (
    <div>
      <NavigationItem label={"Programm"} selected={true} />
    </div>
  );
}
```

### Properties of Props

- Read-Only
- Passed in from outer component

## Built-In Properties

- Components for _HTML_ tags have built-in properties
  - _style_/_className_: styling components
  - _onClick_/_onMouseHover_: mouse interactions
  - any dom attributes are supported (some might behave slightly different)
- Components have a _key_ attribute, which should be used on lists

### Example: Styling

- You can define styling by using an separate css file, and _classnames_

```css, typescript
/* Navigation.tsx: */
import "./styles.css";

export function Navigation() {
  return (
    <div className="Navigation">
      <NavigationItem label={"Programm"} />
    </div>
  );
};

/* styles.css: */
.Navigation {
  display: flex;
  align-items: center;
  justify-content: center
}
```

## Built-In Properties: Children

- All Components have a children property
- This property contains React-Components which are wrapped inside the Component

Example:

```tsx
// component:
export const Navigation = (props: PropsWithChildren) => {
  return <div className="Navigation">{props.children}</div>;
};

// usage:
export function Header() {
  return (
    <Navigation>
      <NavigationItem label={"Programm"} />
      <NavigationItem label={"Speaker"} />
      <NavigationItem label={"FAQ"} />
    </Navigation>
  );
}
```
