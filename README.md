# nakweb

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

# BaseSlider Component

`BaseSlider` is a flexible component for creating sliders.

## Props

| Name            | Type      | Required | Default  | Description                                                                                    |
| --------------- | --------- | -------- | -------- | ---------------------------------------------------------------------------------------------- |
| `totalSlides`   | `Number`  | Yes      | -        | Represents the total number of elements in the slider.                                          |
| `autoPlay`      | `Boolean` | No       | `false`  | Determines if the slider should scroll automatically.                                           |
| `slideDuration` | `Number`  | No       | `3000`   | Duration (in ms) during which each element is displayed when `autoPlay` is enabled.             |
| `control`       | `Boolean` | No       | `true`   | Shows or hides the navigation controls (previous and next buttons).                             |



### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).
