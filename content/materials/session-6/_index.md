---
title: 📊 06 - Instrumental Variables
linkTitle: IVs in R
summary: Welcome to our tutorial about instrumental variables in R
date: '2021-03-15'
type: book
---


{{< toc hide_on="xl" >}}

## Today's session

* Review how to manually extract the LATE through the wald estimator
* Learn how to perform Two-stage Least Squares regression (2SLS) with ivreg() from the AER package
* Illustrate the mechanics of Two-stage Least Squares regression (2SLS) with lm()


<a class="btn btn-success" href="w6_instruments.pdf" role="button" target="_blank">Download slides - PDF</a>

---

### Further references

**For R and RMarkdown** <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Reminder of the basics: https://tinyurl.com/vkebh2f <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`RMarkdown`: The definitive guide https://tinyurl.com/y4tyfqmg <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Data wrangling with `dplyr`: https://tinyurl.com/vyrv596 <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`dplyr` video tutorial: https://www.youtube.com/watch?v=jWjqLW-u3hc <p>

**To explore more about `AER::ivreg()`:**<p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Instrumental variables regression: https://rpubs.com/wsundstrom/t_ivreg 

**For learning more about DAGs and `ggdag`:** <p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;An Introduction to DAGs: https://ggdag.netlify.com/articles/intro-to-dags.html <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Introduction to `ggdag`: https://ggdag.netlify.com/articles/intro-to-ggdag.html <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bias structures: https://ggdag.netlify.com/articles/bias-structures.html <br>
  
 
**Helpful cheatsheets** <p>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Data visualization with `ggplot`: https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Data wrangling with `dplyr` and `tidyr`: https://tinyurl.com/s6zxfqh <br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`RMarkdown` cheatsheet: https://tinyurl.com/uqoelrx <p>

---
<!--
## Meet your instructors


{{< mention "lisa" >}} & {{< mention "sebastian" >}}


## Courses in this program

{{< list_children >}}

{{< figure src="featured.jpg" >}}

{{< callout note >}}
The parameter $\mu$ is the mean or expectation of the distribution.
$\sigma$ is its standard deviation.
The variance of the distribution is $\sigma^{2}$.
{{< /callout >}}
-->
