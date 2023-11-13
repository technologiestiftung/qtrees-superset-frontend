![](https://img.shields.io/badge/Built%20with%20%E2%9D%A4%EF%B8%8F-at%20Technologiestiftung%20Berlin-blue)

<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->

[![All Contributors](https://img.shields.io/badge/all_contributors-0-orange.svg?style=flat-square)](#contributors-)

<!-- ALL-CONTRIBUTORS-BADGE:END -->

# QTrees Superset Frontend

In this repository you will find superset frontend customization description of the QTrees Dashboard.

## Prerequisites

Install the backend described here: https://github.com/technologiestiftung/qtrees-superset

## Installation

The QTrees dashboard uses a Deck.gl Scatterplot for "Baumkarte" that uses custom JS. 
This is the configuration:

![deck.gl configuration](./img/deck-gl.png)

In the **Advanced** section, the following settings are configured:

### Extra data for JS

The columns that have been added are:

- `art_dtsch`
- `standalter`
- `nowcast_value`
- `forecast_value`
- `id`

### JavaScript data interceptor

An interceptor has been added to make the colors of the displayed point a gradient
related to the "saugspannung" rather than the default "random" color set.
This is the snippet:

```JavaScript
(dataArray) => {
      return dataArray.map((dataEntry) => {
            if (!dataEntry.extraProps.nowcast_value) {
                  dataEntry.color = [229, 231, 235, 255]
                  return dataEntry;
            }

            if (dataEntry.extraProps.nowcast_value < 33) {
                  dataEntry.color = [112, 187, 137, 255];
                  return dataEntry;
            }

            if (dataEntry.extraProps.nowcast_value < 81) {
                  dataEntry.color = [224, 215, 126, 255];
                  return dataEntry;
            }

            dataEntry.color = [254, 172, 118, 255];
            return dataEntry;
      })
}
```

### JavaScript tooltip generator

The tooltip has been adjusted to fill it with more useful information, 
such as the tree species, its age and its suction tension. 
This is the snippet:

```JavaScript
(dataEntry) => {
      const saugspannungLabelNow = dataEntry.object.extraProps.nowcast_value ? `${dataEntry.object.extraProps.nowcast_value} kPa` : '';
      const saugspannungLabelForecast = dataEntry.object.extraProps.forecast_value ? `${dataEntry.object.extraProps.forecast_value} kPa` : '';
      return `${dataEntry.object.extraProps.art_dtsch}, ${dataEntry.object.extraProps.standalter} Jahre <br> Saugspannung (heute): ${saugspannungLabelNow} <br> Sauspannung (14 Tage): ${saugspannungLabelForecast} <br> Id: ${dataEntry.object.extraProps.id}`;
}

```

### Styling adjustments

We changed the styling to match the QTrees UI a bit more. This happens in several places:

#### Additional CSS snippet

1. In your dashboard, click on "Edit dashboard"
2. Click on the three dots that appear, next to the "Save" button
3. In the dropdown click on "Edit CSS"
4. Insert the following CSS

```css
.css-jysgjt.grid-column > :not(.hover-menu):not(:last-child) {
  margin-bottom: 0px;
}

.dashboard-chart-id-4 {
  padding-bottom: 0px !important;
}

.dashboard-chart-id-2 {
  padding-top: 0px !important;
}

.css-13rbkvc{
  padding-bottom: 0px !important;
}

/* Light general background */
body {
  background-color: #70bb890D;
}

/* Custom font - taken from https://preset.io/blog/customizing-superset-dashboards-with-css/#general-backgrounds-fonts-and-colors  */
@import url('https://baumblick.qtrees.ai/fonts/Manrope/Manrope-VariableFont_wght.woff2?v=3.18');

body {
  font-family: 'Manrope', sans-serif !important;
  font-weight: 500;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

/* remove spacing between Saugspannung header and description  */
.dragdroppable-row {
  margin-bottom: 0 !important;
}

/* Tab re-coloring  */
.ant-tabs-card > .ant-tabs-nav .ant-tabs-tab-active, .ant-tabs-card > div > .ant-tabs-nav .ant-tabs-tab-active {
  color: #70bb89 !important;
}

.ant-tabs-tab:hover {
  color: #70bb89 !important;
}

.ant-tabs-ink-bar {
  background-color: #70bb89 !important;
}

/* track filter re-coloring */
.ant-slider-track {
  background-color: #70bb89 !important;
}

.ant-slider-handle {
  border-color: #70bb89 !important;
}

.filter-apply-button:not([disabled]) {
  background-color: #70bb89 !important;
}


/* colorful panels for charts  */

.css-c7w8t3 :nth-of-type(1) {
    background-color: #70bb89;
    opacity: 0.12;
  }

/* Baumdetails Liste
.dashboard-chart-id-9 {
  background-color: #70bb891a !important;
}

/* Verschattung
.dashboard-chart-id-18 {
  background-color: #feac761a !important;
}
*/

/* increase font size of Baumdetails heading  */
.dashboard-chart-id-9 .header-title {
  font-size: 24px !important;
  margin-bottom: 12px;
}
```

#### Dashboard theme

We also adjusted the theme slightly.

1. In your dashboard, click on "Edit dashboard"
2. Click on the three dots that appear, next to the "Save" button
3. In the dropdown click on "Edit properties"
4. In the modal, click on "Advanced"
5. Insert the following key value pair into the JSON metadata field:

```json
"label_colors": {
    "30": "#ffebb8",
    "60": "#fdd19b",
    "90": "#feac76",
    "Temperatur in °C": "#feac76",
    "Niederschlag in mm": "#1a85a0",
    "Wind in m/s": "#99e7f0",
    "AVG(nowcast_value)": "#99e7f0"
  },
```

## Contributing

Before you create a pull request, write an issue, so we can discuss your changes.

## Contributors

Thanks goes to these wonderful people ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tr>
  </tr>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

This project follows the [all-contributors](https://github.com/all-contributors/all-contributors) specification. Contributions of any kind welcome!

## Content Licensing

Texts and content available as [CC BY](https://creativecommons.org/licenses/by/3.0/de/).

Illustrations by {MARIA_MUSTERFRAU}, all rights reserved.

## Credits

<table>
  <tr>
    <td>
      Made by <a href="https://citylab-berlin.org/de/start/">
        <br />
        <br />
        <img width="200" src="https://citylab-berlin.org/wp-content/uploads/2021/05/citylab-logo.svg" />
      </a>
    </td>
    <td>
      A project by <a href="https://www.technologiestiftung-berlin.de/">
        <br />
        <br />
        <img width="150" src="https://citylab-berlin.org/wp-content/uploads/2021/05/tsb.svg" />
      </a>
    </td>
    <td>
      Supported by <a href="https://www.berlin.de/rbmskzl/">
        <br />
        <br />
        <img width="80" src="https://citylab-berlin.org/wp-content/uploads/2021/12/B_RBmin_Skzl_Logo_DE_V_PT_RGB-300x200.png" />
      </a>
    </td>
  </tr>
</table>

## Related Projects
[QTrees Superset Backend](https://github.com/technologiestiftung/qtrees-superset)