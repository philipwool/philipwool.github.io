---
title: Ryan Wooldridge's Portfolio
---
<!--This is the first row of projects -->
<div style="display:table-row; width:100%; table-layout: fixed">
<div style="display: table-cell; width:370px; margin-right:3px" markdown="1">

### Project 1 

![It's Fine Alt Text](https://philipwool.github.io/project1/Hex_Analysis_screenshot.png)

[See more details here.](https://philipwool.github.io/project1/project1.html)

Spatial distribution analysis of the density of $250,000 homes in Baltimore city.

Using SQL to query a Spatialite database:

```html
select st_centroid(GEOMETRY) from real_property_database where salepric >= 250000 and usegroup = 'R'
```

<small>__Tools__: QGIS, SQL</small>

<small>__Data__: 
[Supportland](https://supportland.com/), [Oregon Craft Brew Guild](https://oregoncraftbeer.org/guild/)</small>

</div>

<div style="display: table-cell; width:370px" markdown="1">

### Project 2

![It's Fine Alt Text](https://philipwool.github.io/project2/3d_Comm.gif)

[See more details here.](https://philipwool.github.io/project2/project2.html)

Spatial and temporal distribution analysis of commercial development in Baltimore city.

Using Python to write new shapefiles from a spatial query selection:

```html
selection = Real_Property.getFeatures(QgsFeatureRequest(). setFilterExpression(u'"YEAR_BUILD" >= 1900 and "YEAR_BUILD" <= 2018 and "USEGROUP" = \'C\''))
```

Notice I used markdown inside the html tags. 

<small>__Tools__: QGIS, Python, Photoshop</small>

<small>__Data__:
[Census Streets](https://www.census.gov/cgi-bin/geo/shapefiles/index.php), US Business Directory (defunct)</small>

</div>
</div>
<!--This is the second row of projects -->
<div style="display:table-row; width:100%; table-layout: fixed">
<div style="display: table-cell; width:370px; margin-right:3px" markdown="1">

### Lab 6 

![It's Fine Alt Text](philipwool.github.io/lab6/Guerry_Dotn_NatBrk.JPG)

[See more details here.](https://philipwool.github.io/lab6/lab6.html)

This project uses a 350px square image for the teaser image, but inside the square image, I used a circle to highlight a certain area. Pellentesque eget mauris vel mi tristique finibus vitae quis massa. Mauris vulputate, nulla vel tincidunt interdum, sem mauris scelerisque neque, suscipit pellentesque felis augue a erat. 

<small>__Tools__: GeoDa

<small>__Data__: 
[Supportland](https://supportland.com/), [Oregon Craft Brew Guild](https://oregoncraftbeer.org/guild/)</small>

</div>

<div style="display: table-cell; width:370px" markdown="1">

### Project 3

![It's Fine Alt Text](project4_demo/p4_teaser.png)

[See more details here.](https://dillonma.github.io/project2_sfi/project2.html)

Phasellus consequat quam elit, et iaculis risus pellentesque aliquet. Proin ut enim dui. Ut elementum, purus nec rhoncus sagittis, nibh nunc auctor nulla, eu condimentum nisi velit eget magna. Nulla feugiat tincidunt dictum. Vestibulum congue sapien elit. Maecenas non sodales ligula, quis tempor mi. 

<small>__Tools__: QGIS, ArcGIS, Python

<small>__Data__:
[Census Streets](https://www.census.gov/cgi-bin/geo/shapefiles/index.php), US Business Directory (defunct)</small>

</div>
</div>

<!--This is just other markdown -->

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/dillonma/dillonma.github.io/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
