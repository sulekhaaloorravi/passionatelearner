## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/sulekhaaloorravi/passionatelearner/edit/master/README.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

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

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/sulekhaaloorravi/passionatelearner/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.

---
title: "SulekhaAloorravi_SL_ASmt"
output: html_notebook
---

A. Create a full factorial design for a product with 5 attributes and 2 levels each. Level for each attribute can be labelled 1 and 2.

```{r}
library(conjoint)
Brand <- c("LG", "Whirlpool")
Capacity_Litres <- c("190","240")
Price <- c(15290,23900)
Appearance <- c("SingleDoorScarlet","DoubleDoorSteel")
DefrostSystem <- c("DirectCool", "FrostFree")

FullFactorial<- expand.grid(Brand,Capacity_Litres,Price,Appearance,DefrostSystem)
FullFactorialDesign <- caFactorialDesign(FullFactorial,type="full")
colnames(FullFactorialDesign) <- c("Brand", "Capacity in Liters", "Price", "Appearance", "Defrost System")

FullFactorialDesign$Price <- as.factor(FullFactorialDesign$Price)

View(FullFactorialDesign)

NumberOfProfiles = nrow(FullFactorialDesign)

print(c("Number Of Profiles = ",NumberOfProfiles))

caEncodedDesign(FullFactorialDesign) -> EncodedFullProfile

View(EncodedFullProfile)

cor(EncodedFullProfile)

Ravi <- sample(1:32,32)
  
Dileep <- sample(1:32,32)
  
Sasi <- sample(1:32,32)
  
Sailu <- sample(1:32,32)
  
Praba <- sample(1:32,32)
  
Sudha <- sample(1:32,32)  

ConsumerRanks <- rbind(Ravi,Dileep,Sasi,Sailu,Praba,Sudha)

Levels <- c(Brand,Capacity_Litres,Price,Appearance,DefrostSystem)

caModel(Ravi,EncodedFullProfile)

caPartUtilities(ConsumerRanks,EncodedFullProfile,Levels)

caSegmentation(ConsumerRanks,EncodedFullProfile)

caImportance(ConsumerRanks,EncodedFullProfile)

caImportance(Ravi,EncodedFullProfile)

```

B.Create an orthogonal design, how many profiles are there?

```{r}
OrthogonalProfiles <- caFactorialDesign(EncodedFullProfile,type="orthogonal")

View(OrthogonalProfiles)

cor(OrthogonalProfiles)

NumberOfProfiles = nrow(OrthogonalProfiles)

print(c("Number Of Profiles = ",NumberOfProfiles))

Ravi <- sample(1:8,8)
  
Dileep <- sample(1:8,8)
  
Sasi <- sample(1:8,8)
  
Sailu <- sample(1:8,8)
  
Praba <- sample(1:8,8)
  
Sudha <- sample(1:8,8)  

ConsumerRanks <- rbind(Ravi,Dileep,Sasi,Sailu,Praba,Sudha)

Levels <- c(Brand,Capacity_Litres,Price,Appearance,DefrostSystem)

caModel(Ravi,OrthogonalProfiles)

caPartUtilities(ConsumerRanks,OrthogonalProfiles,Levels)

caSegmentation(ConsumerRanks,OrthogonalProfiles)

caImportance(ConsumerRanks,OrthogonalProfiles)

caImportance(Ravi,OrthogonalProfiles)

```

C. consumers’ willingness to pay for color given the following output of a conjoint analysis. Price has three levels and color has two levels.  Price levels are 50, 100, and 150.  Color levels are Black and White.
The coefficients estimated by caModel function are given below.
Price 50    7.8  (*Price levels should be 50 and 100)
Price 100    0.8
Colour Black   1.4

Explanation;

In conjoin analysis, sum total of all co-efficients for an attribute should be equal to 0.

In this case, there are 3 levels for Price - 50, 100, 150.
Co-efficients for:
Price 50 = 7.8
Price 100 = 0.8

```{r}
PriceData = c(50,100,150)
Price50 = 7.8
Price100 = 0.8
#Calculating Coefficient of Price 150
Price150 = 0 - (Price100+Price50)
Price150
#Calculating Range of Price
Range.CoeffPrice = Price50-Price150
Range.CoeffPrice

Range.Price = max(PriceData) - min(PriceData)

UnitSatisfaction = Range.Price/Range.CoeffPrice
UnitSatisfaction

#Calculating Willingness to pay for color
ColorBlack = 1.4

#Color white as per conjoint analysis sum total of coefficients will be
ColorWhite = 0-ColorBlack
ColorWhite

#Range of coefficient of color:
Range.CoeffColor = ColorBlack - ColorWhite

#Willingess to Pay for Color
WIP.Color = UnitSatisfaction * Range.CoeffColor

```




