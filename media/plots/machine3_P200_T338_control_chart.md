library(tidyverse)
library(plotly)
library(htmlwidgets)

TARGET_MACHINE <- 3
TARGET_PRESSURE <- 200
TARGET_TEMPERATURE <- 338

TARGET_VALUE <- 50
USL <- 55
LSL <- 45

df_filtered <- X039 %>%
  filter(Machine == TARGET_MACHINE,
         Pressure == TARGET_PRESSURE,
         Temperature == TARGET_TEMPERATURE)

metric_data <- df_filtered$PartLength

sample_mean <- mean(metric_data)
sample_sd <- sd(metric_data)

UCL <- sample_mean + 3 * sample_sd
LCL <- sample_mean - 3 * sample_sd

control_chart_data <- data.frame(
  Index = 1:length(metric_data),
  PartLength = metric_data,
  Mean = sample_mean,
  UCL = UCL,
  LCL = LCL
)

p_control <- plot_ly(control_chart_data, type = "scatter", mode = "lines+markers") %>%
  add_trace(y = ~PartLength, name = "Individual Measurements", marker = list(color = "#0072B2")) %>%
  add_trace(y = ~Mean, name = "Mean", mode = "lines", line = list(color = "#009E73", dash = "dash", width = 2), showlegend = TRUE) %>%
  add_trace(y = ~UCL, name = "UCL (3sigma)", mode = "lines", line = list(color = "#D55E00", dash = "dot", width = 2), showlegend = TRUE) %>%
  add_trace(y = ~LCL, name = "LCL (3sigma)", mode = "lines", line = list(color = "#D55E00", dash = "dot", width = 2), showlegend = TRUE) %>%
  layout(
    title = list(text = paste0("Control Chart for PartLength (Machine ", TARGET_MACHINE, ", P=", TARGET_PRESSURE, "kPa, T=", TARGET_TEMPERATURE, "K)"), font = list(size = 20)),
    xaxis = list(title = list(text = "Observation Index", font = list(size = 18)), tickfont = list(size = 14)),
    yaxis = list(title = list(text = "PartLength", font = list(size = 18)), tickfont = list(size = 14)),
    plot_bgcolor = "white",
    paper_bgcolor = "white",
    legend = list(orientation = "h", xanchor = "center", x = 0.5),
    hovermode = "x unified"
  )

htmlwidgets::saveWidget(p_control, paste0("media/plots/machine3_P200_T338_control_chart.html"), selfcontained = TRUE)
