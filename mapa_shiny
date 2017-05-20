require(shiny)
require(choroplethr)
require(choroplethrMaps)
require(gdata)

life_expectancy=read.csv("https://raw.githubusercontent.com/drusyn/mapa/master/life%20expectancy.csv")
for (i in 261:999) {
  life_expectancy=life_expectancy[-261,]
}
rm(i)
colnames(life_expectancy) = c("Life expectancy", substr(colnames(life_expectancy)[2:218], 2, 5))
life_expectancy[,1]=tolower(life_expectancy[,1])
years=as.numeric(c(colnames(life_expectancy)[2:218]))
life_expectancy$`Life expectancy`[241]="united states of america"
life_expectancy$`Life expectancy`[133]="macedonia"
life_expectancy$`Life expectancy`[200]="republic of serbia"
life_expectancy$`Life expectancy`[206]="slovakia"
life_expectancy$`Life expectancy`[226]="east timor"
life_expectancy$`Life expectancy`[224]="united republic of tanzania"
life_expectancy$`Life expectancy`[17]="the bahamas"
life_expectancy$`Life expectancy`[54]="ivory coast"
life_expectancy$`Life expectancy`[50]="democratic republic of the congo"
life_expectancy$`Life expectancy`[51]="republic of congo"
life_expectancy$`Life expectancy`[120]="kosovo"
life_expectancy$`Life expectancy`[122]="kyrgyzstan"
life_expectancy$`Life expectancy`[123]="laos"
life_expectancy$`Life expectancy`[94]="guinea bissau"

ui<-shinyUI(fluidPage(
  titlePanel("Oczekiwana długość życia w krajach na świecie w latach 1800-2016"),
  sidebarLayout(
    sidebarPanel(
      sliderInput("year",
                  "Wybierz rok",
                  min = min(years),
                  max = max(years),
                  value = median(years),
                  sep="")
    ),
    
    mainPanel(
      plotOutput("mapPlot")
    )
  )
))

server <- shinyServer(function(input, output) {
  output$mapPlot <- renderPlot({
    plot_data=as.data.frame(life_expectancy[,1])
    colnames(plot_data)=c("region")
    plot_data$value=life_expectancy[,input$year-1798]
    country_choropleth(plot_data, paste("Rok", input$year))
  })
  
}
)
shinyApp(ui, server)
