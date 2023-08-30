# Assignment 1
You may use any software to create your document (e.g., Microsoft Word, Google Docs, LaTeX, Markdown, etc.), but submit your assignment as a PDF.

## Problem set 1
The main theme of this course is that ecology is the study of connections between things in nature. In this exercise, you will learn about a peer-reviewed publication that proposes a hypothesis about how weather patterns are connected to mosquito population dynamics. You will then build on this idea yourself, by looking for further connections between weather patterns and mosquito-borne diseases in human populations using some simple data analysis.

### 1.1 Introduction
This exercise is based on an idea proposed by Jon Chase and Tiffany Knight in 2003. For more details, see: Drought-induced mosquito outbreaks in wetlands. *Ecology Letters* 6: 1017–1024. I have placed this optional reading in `Files` on Canvas.

In the paper, Chase and Knight propose the idea that episodes of drought result in **increased** mosquito populations the following year in wetlands that dry periodically (called semi-permanent wetlands). This is a bit weird and maybe the opposite of what you'd expect. Mosquitos lay eggs in temporary water bodies where the larvae and pupae form before emerging from the water as flying (and biting!) adults. Intuition suggests wet years would be beneficial, since more precipitation means more habitat for egg-laying!

Instead, the authors suggest that it is species interactions - specifically, predation and competition - that limit larval mosquito populations in wetlands. To explore this idea, they divided a bunch of wetlands into three types by how frequently they dry out: permanent wetlands that never dry, temporary wetlands that dry every year, and semi-permanent wetlands that dry only during drought years.

In permanent wetlands, there are always many predators and competitors that limit larval mosquito survival such as mosquitofish eating mosquito larvae. Similarly, in temporary wetlands, there is a suite of competitors that are adapted to annual drying that compete with and limit survival of larval mosquitoes. Zooplankton are competitors in temporary wetlands. However, in semi-permanent wetlands, few competitors and predators are adapted to rapid recolonization after periodic drought and drying episodes. After a drought, when the semi-permanent wetlands refill, mosquitoes quickly recolonize and exploit the food resources there, producing a spike in populations before competitors or predators are able to recolonize. Thus, the lack of competitors in the year following a drought produces large mosquito populations in such wetlands.

One of the connections highlighted in Chapter 1 is that between human activities and West Nile virus (WNV). West Nile virus can cause severe sickness in humans. It was first identified in the Congo in the 1930s, and subsequently spread nearly worldwide in temperate and tropical areas. It was first documented in the U.S. in New York in 1999. West Nile virus is transmitted by infected mosquitoes (mainly genus Culex) when they bite humans.

We are interested in exploring the connection between climate variation, specifically drought periods and the incidence of this mosquito-borne disease. Because of the relationship between mosquito outbreaks and drought identified in the paper we reviewed, and the suggestion that higher populations of mosquitoes should result in higher incidence of West Nile virus in humans, we can predict that WNV outbreaks might follow severe droughts. We will explore these connections by comparing patterns of drought to patterns of WNV incidence. The most reliable measure of drought is the Palmer Drought Severity Index (PDSI). The Palmer Drought Severity Index incorporates both temperature and precipitation into a single index. Positive values of PDSI indicate wet periods and negative values indicate drought.

We want to determine whether there might be a relationship between severe drought and the incidence of mosquito-borne diseases. The reasoning is that in the year after a drought, the larger mosquito populations from semi-permanent wetlands would be more likely to result in transmission of mosquito-borne diseases. 

*Your job is to test for a relationship between drought and incidence of West Nile disease by plotting mean PDSI (lagged by one year) on the x-axis and number of reported cases of WNV on the y-axis for a bunch of real wetlands*. The term "lagged by one year" means we match the PDSI from one year to the next year's number of WNV cases.

### 1.2 Performing a simple data analysis
You may use any software to perform the data analysis for this assignment, including Excel. Many if not most biologists across academia and industry use the `R` programming language to do various statistical and computational things. It is capable of everything from functioning like a routine graphing calculator (like a TI-83), to performing state-of-the-art machine learning on massive datasets. We will occasionally use `R` in this course to do various computations for us. Fortunately, there are tools these days to run `R` code directly in a web browser. Of course, you can [feel free to install](https://www.r-project.org/) the `R` programming language directly on your computer. But, it is much easier to use the web-based application. *Note:* I don't expect you to learn computer programming in this course. What I do expect is that you can [1] copy-paste code that I provide into the web app, [2] occasionally customize the code that I provide slightly, [3] run the code, and [4] make sense of the output or results.

The web app can be accessed by going to [https://rdrr.io/snippets/](https://rdrr.io/snippets/). When you go to the website, you will see some example generic code already. Go ahead and **delete** all of it to start with a blank console. Next go ahead and copy-paste the code snippet below into the blank console. But do not run the code snippet quite yet (*see below*).

```r
## Choose my custom color
myColor = "#000000"

## Input my data
droughtSeverity = c(-1.863, -1.525, 2.221, 4.504, 0.1, 1.177, 0.325, 0.243, 0.364, -0.419, 3.404, -0.136, 0.428, 0.736, -0.298, -1.273, 1.163)
westNileCases   = c(62, 237, 15, 25, 9, 10, 14, 0, 28, 6, 60, 11, 13, 30, 16, 20, 130)

## Plot my data, and add a trendline in red
plot(westNileCases ~ droughtSeverity, pch = 16, cex = 2, bty = 'l', xlab = 'Drought severity index', ylab = 'West Nile cases')
abline(lm(westNileCases ~ droughtSeverity), col = myColor, lwd = 3)

## Slope of the trend line
cor(droughtSeverity, westNileCases)
```

Before you perform hit `Run` to do this data analysis, I want you to add your own aesthetic. You can do this by choosing a *unique* color that you like when plotting your data figure. Go to [https://htmlcolorcodes.com/](https://htmlcolorcodes.com/) and play with the color sliders until you are satisfied with your color. Then copy the `HEX` code for your color and paste it in your code snippet on the line that reads `myColor = "#000000"` making sure it is inside quotes. For example, if my chosen color's hex code is `#21674c`, the line in my code block would look like `myColor = "#21674c"`.

#### Question 1.1
Once you've chosen your custom color, run the entire code snippet by clicking the `Run` button or pressing `CMD-Enter`. Right click on the plot to save your results, and record the slope of the trend line (this is the value that is output-ed with your graph). Give me the hex code for your chosen color, the slope of the trend line, and your data figure.

#### Question 1.2
Do you see evidence of a link between severe drought and WNV? What features of your data figure support your argument? When are the highest WNV rates typically seen in these data?

#### Question 1.3
What might be a limitation of using the pattern observed by Chase and Knight to infer incidence of disease by mosquito vectors?


## Problem set 2
Create a document highlighting a plant and the biome it represents.

Go outside in your neighborhood or a favorite park or outdoor area with lots of plants. Once there, take pictures of a plant that represents the typical growth form of a particular biome that you would like to feature (review these in Ch. 3). If you don’t have access to a spot with different plant types, you can look up plants in nearby areas using [iNaturalist](https://www.inaturalist.org/). 

Use the [interactive biome viewer](https://www.biointeractive.org/classroom-resources/biomeviewer) to find a place in the world that has the biome you are featuring. Open the web page and click on "Start Interactive".

The different colors represent different biomes, as is shown at the left of the screen. Click and drag the globe to find a place that contains the particular biome you are highlighting, and click on it to drop a pin. A description of the place and the climatogram will appear on the right. Take a screen shot including the globe and all the information on the right side.

#### Question 2.1
Provide a picture of the plant (in focus and showing enough detail we can see the example of the growth form). You do not need to identify it to species, but if you know what type of plant it is aside from the growth form, go ahead and include that information.

#### Question 2.2
Tell me the name of the biome you are featuring. 

#### Question 2.3
Name the climactic features of the biome that lead to the growth form (i.e temperature and rainfall). Tell me growth form. And point out one feature in the picture of the plant that is an example of the growth form.

#### Question 2.4
Provide the screen shot from biome viewer of your example biome.
