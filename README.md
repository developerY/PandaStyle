# PandaStyle
# Aligned Gradient Bars in Pandas DataFrames

## Introduction
This repository demonstrates how to create **aligned gradient bars** within a Pandas DataFrame for visually intuitive data representation. The approach ensures consistent alignment of color bands across rows using modern CSS techniques like `linear-gradient` and `clip-path`. The resulting visualization is clear, aesthetically pleasing, and works seamlessly in Jupyter Notebooks or as exported HTML.

## Features
- **Aligned Color Gradients**: Colors remain consistent across rows, regardless of bar length.
- **Dynamic Truncation**: Gradient bars adjust proportionally to the values.
- **Gray Background**: Enhances clarity by framing each gradient bar.
- **Value Overlay**: Displays the numeric value in bold, centered over the gradient.
- **Browser Compatibility**: Supports modern browsers with `linear-gradient` and optionally `-webkit-gradient` for older WebKit browsers.

## Requirements
- Python 3.6+
- Pandas
- Jupyter Notebook (optional, for interactive use)

## Installation
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-folder>
   ```

2. Install required Python packages:
   ```bash
   pip install pandas
   ```

## Usage
### Example DataFrame Visualization
The script dynamically generates gradient bars for a sample DataFrame based on the `Value` column. Adjustments can be made to column names, data, and gradient styling.

```python
import pandas as pd
from IPython.core.display import display, HTML

# Sample DataFrame
data = {
    "Metric": [f"Metric {i}" for i in range(1, 6)],
    "Value": [0, 25, 50, 75, 100],
}
df = pd.DataFrame(data)

# Function to style DataFrame
from gradient_bars import style_corrected_gradient_gauge
styled_df = style_corrected_gradient_gauge(df)

# Display styled DataFrame
display(HTML(styled_df.to_html()))
```

### Gradient Bar CSS Logic
The gradient bar uses a **full-spectrum gradient** as the baseline and dynamically truncates the visible section using `clip-path`:

```python
def generate_corrected_gradient_css(value):
    return (
        "background: linear-gradient(to right, red 0%, yellow 25%, lightgreen 75%, green 100%); "
        f"clip-path: inset(0 {100 - value}% 0 0); "  # Dynamically crop the gradient
        "height: 100%;"
    )
```

### Exporting to HTML
The styled table can be exported as an HTML file:

```python
output_file = "aligned_gradient_bars.html"
with open(output_file, "w") as f:
    f.write(styled_df.to_html())
print(f"HTML file saved as: {output_file}")
```

## Examples
### Output Example
| Metric   | Value                                          |
|----------|-----------------------------------------------|
| Metric 1 | Fully gray (value = 0).                      |
| Metric 2 | Red band extending to 25%, aligned with the spectrum. |
| Metric 3 | Red → Yellow band extending to 50%.           |
| Metric 4 | Red → Yellow → Light Green band extending to 75%. |
| Metric 5 | Full spectrum (Red → Yellow → Light Green → Green).    |

### Browser Preview
The exported HTML file can be opened in any modern browser for a visual preview of the aligned gradient bars.

## Customization
1. **Colors**: Modify the gradient colors in `generate_corrected_gradient_css`.
2. **Widths**: Adjust column widths in the `style_corrected_gradient_gauge` function by editing CSS properties.
3. **Data**: Replace the sample DataFrame with your own dataset.

## Contributing
Contributions are welcome! Feel free to submit pull requests for improvements, bug fixes, or new features.

## License
This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## Acknowledgments
Thanks to CSS and Pandas for making powerful visualizations possible. Special thanks to modern browser developers for supporting features like `linear-gradient` and `clip-path`. 🚀

