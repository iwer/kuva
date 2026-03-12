# Ridgeline Plot

A ridgeline plot (also called a joyplot) stacks multiple KDE density curves vertically — one per group. Groups are labelled on the y-axis; the x-axis is the continuous data range. Curves can overlap for the classic "mountain range" look.

## Basic Example

```rust,no_run
use kuva::plot::ridgeline::RidgelinePlot;
use kuva::render::plots::Plot;
use kuva::render::layout::Layout;
use kuva::render::render::render_multiple;
use kuva::backend::svg::SvgBackend;

let plot = RidgelinePlot::new()
    .with_group("Control", vec![1.2, 1.5, 1.8, 2.0])
    .with_group("Treated", vec![3.5, 4.0, 4.5, 5.0]);

let plots = vec![Plot::Ridgeline(plot)];
let layout = Layout::auto_from_plots(&plots)
    .with_title("Expression by Group")
    .with_x_label("Value");
let svg = SvgBackend.render_scene(&render_multiple(plots, layout));
```

## CLI

```bash
kuva ridgeline samples.tsv --group-by group --value expression \
    --title "Ridgeline" --x-label "Expression"
```

## Options

| Method | Default | Description |
|--------|---------|-------------|
| `.with_group(label, data)` | — | Append a group |
| `.with_group_color(label, data, color)` | — | Append a group with explicit color |
| `.with_groups(iter)` | — | Add multiple groups at once |
| `.with_filled(bool)` | `true` | Fill the area under each curve |
| `.with_opacity(f64)` | `0.7` | Fill opacity |
| `.with_overlap(f64)` | `0.5` | Fraction of cell height ridges may overlap |
| `.with_bandwidth(f64)` | Silverman | KDE bandwidth |
| `.with_kde_samples(usize)` | `200` | Number of KDE evaluation points |
| `.with_stroke_width(f64)` | `1.5` | Outline stroke width |
| `.with_normalize(bool)` | `false` | Use PDF normalization instead of visual scaling |
| `.with_legend(bool)` | `false` | Show a legend (y-axis labels are usually sufficient) |
| `.with_line_dash(str)` | — | SVG stroke-dasharray for dashed outline |
