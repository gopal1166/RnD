### 1. Adding filter effect to background image:

[link](https://www.w3schools.com/howto/howto_css_image_effects.asp)
```
 filter: grayscale(100%);
 ```


### 2. Image overly color css: (Tor write text on image)
[link](https://dev.to/ellen_dev/two-ways-to-achieve-an-image-colour-overlay-with-css-eio)

```
header {
    height: 600px;
    width: 100vw;
    background: black;
    overflow: hidden;
    background: #C33764;  /* fallback colour. Make sure this is just one solid colour. */
    background: -webkit-linear-gradient(rgba(29, 38, 113, 0.8), rgba(195, 55, 100, 0.8)), url("https://bit.ly/2rlzaXi");
    background: linear-gradient(rgba(29, 38, 113, 0.8), rgba(195, 55, 100, 0.8)), url("https://bit.ly/2rlzaXi"); /* The least supported option. */
}

img {
   object-fit: cover;
}
```

#### Color tranisition in background overlay:
```
header {
    height: 600px;
    width: 100vw;
    background: black;
    overflow: hidden;
    background: #C33764;  /* fallback colour. Make sure this is just one solid colour. */
    background: -webkit-linear-gradient(rgba(29, 38, 113, 0.8), rgba(195, 55, 100, 0.8)), url("https://bit.ly/2rlzaXi");
    background: linear-gradient(rgba(29, 38, 113, 0.8), rgba(195, 55, 100, 0.8)), url("https://bit.ly/2rlzaXi"); /* The least supported option. */
}

img {
   object-fit: cover;
}
```
