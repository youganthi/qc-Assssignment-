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
  UCL <- mu + 3 * sigma
  LCL <- mu - 3 * sigma

  control_chart_data <- data.frame(
    Index = 1:n,
    PartLength = metric_data,
    Mean = mu,
    UCL = UCL,
    LCL = LCL
  )

  p_control <- plot_ly(control_chart_data, type = "scatter", mode = "lines+markers") %>%
    add_trace(y = ~PartLength, name = "Individual Measurements", marker = list(color = "#0072B2"), line = list(color = "#0072B2")) %>%
    add_trace(y = ~Mean, name = "Mean", mode = "lines", line = list(color = "#009E73", dash = "dash", width = 2), showlegend = TRUE) %>%
    add_trace(y = ~UCL, name = "UCL (3σ)", mode = "lines", line = list(color = "#D55E00", dash = "dot", width = 2), showlegend = TRUE) %>%
    add_trace(y = ~LCL, name = "LCL (3σ)", mode = "lines", line = list(color = "#D55E00", dash = "dot", width = 2), showlegend = TRUE) %>%
    layout(
      title = list(text = paste0("Control Chart for PartLength (Machine ", TARGET_MACHINE, ", P=", TARGET_P, "kPa, T=", TARGET_T, "K)"), font = list(size = 20)),
      xaxis = list(title = list(text = "Observation Index", font = list(size = 18)), tickfont = list(size = 14)),
      yaxis = list(title = list(text = "PartLength", font = list(size = 18)), tickfont = list(size = 14)),
      plot_bgcolor = "white",
      paper_bgcolor = "white",
      legend = list(orientation = "h", xanchor = "center", x = 0.5),
      hovermode = "x unified"
    )

  htmlwidgets::saveWidget(p_control, paste0("media/plots/machine", TARGET_MACHINE, "_control_chart.html"), selfcontained = TRUE)
}

