library(tidyverse)
library(plotly)
library(htmlwidgets)

TARGET_MACHINE <- 1
TARGET_P <- 200
TARGET_T <- 338
Target <- 50
USL <- 55
LSL <- 45

df_filtered <- X039 %>%
  filter(Machine == TARGET_MACHINE,
         Pressure == TARGET_P,
         Temperature == TARGET_T)
metric_data <- df_filtered$PartLength

if(length(metric_data) > 0) {
  n <- length(metric_data)
  mu <- mean(metric_data)
  sigma <- sd(metric_data)
  cpk_usl <- (USL - mu) / (3 * sigma)
  cpk_lsl <- (mu - LSL) / (3 * sigma)
  Cpk <- min(cpk_usl, cpk_lsl)

  x_min <- min(metric_data, LSL, USL) - 2 * sigma
  x_max <- max(metric_data, LSL, USL) + 2 * sigma
  x_density <- seq(x_min, x_max, length.out = 500)
  y_density <- dnorm(x_density, mean = mu, sd = sigma)

  p_capability <- plot_ly(alpha = 0.6) %>%
    add_histogram(x = ~metric_data, name = "Observed Data", marker = list(color = "#0072B2", line = list(color = "black", width = 0.5)), histnorm = "probability density") %>%
    add_lines(x = ~x_density, y = ~y_density, name = "Fitted Normal Distribution", line = list(color = "black", dash = "dash", width = 2)) %>%
    add_segments(x = LSL, xend = LSL, y = 0, yend = max(y_density)*1.1, name = "LSL", line = list(color = "#D55E00", width = 3)) %>%
    add_segments(x = USL, xend = USL, y = 0, yend = max(y_density)*1.1, name = "USL", line = list(color = "#D55E00", width = 3)) %>%
    add_segments(x = Target, xend = Target, y = 0, yend = max(y_density)*1.1, name = "Target", line = list(color = "#CC79A7", dash = "dash", width = 2)) %>%
    layout(
      title = list(text = paste0("Process Capability for PartLength (Machine ", TARGET_MACHINE, ", P=", TARGET_P, "kPa, T=", TARGET_T, "K)"), font = list(size = 20)),
      xaxis = list(title = list(text = "PartLength", font = list(size = 18)), tickfont = list(size = 14), zeroline = FALSE, showgrid = FALSE),
      yaxis = list(title = list(text = "Density", font = list(size = 18)), tickfont = list(size = 14), zeroline = FALSE, showgrid = FALSE),
      plot_bgcolor = "white",
      paper_bgcolor = "white",
      bargap = 0.1,
      showlegend = TRUE,
      legend = list(orientation = "h", xanchor = "center", x = 0.5),
      hovermode = "x unified"
    )

  htmlwidgets::saveWidget(p_capability, paste0("media/plots/machine", TARGET_MACHINE, "_capability_chart.html"), selfcontained = TRUE)
}

