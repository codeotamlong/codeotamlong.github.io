---
title: Text and Typography
author: cotes
date: 2019-08-08 11:33:00 +0800
categories: [Blogging, Demo]
tags: [typography]
pin: true
math: true
mermaid: true
image:
  path: /assets/img/text-and-typography/devices-mockup.png
  lqip: data:image/webp;base64,UklGRpoAAABXRUJQVlA4WAoAAAAQAAAADwAABwAAQUxQSDIAAAARL0AmbZurmr57yyIiqE8oiG0bejIYEQTgqiDA9vqnsUSI6H+oAERp2HZ65qP/VIAWAFZQOCBCAAAA8AEAnQEqEAAIAAVAfCWkAALp8sF8rgRgAP7o9FDvMCkMde9PK7euH5M1m6VWoDXf2FkP3BqV0ZYbO6NA/VFIAAAA
  alt: Responsive rendering of Chirpy theme on multiple devices.
---

This post is to show Markdown syntax rendering on [**Chirpy**](https://github.com/cotes2020/jekyll-theme-chirpy/fork), you can also use it as an example of writing. Now, let's start looking at text and typography.

## Headings

```markdown
## Headings
```
{: file="Cú pháp"}

# H1 - heading
{: .mt-4 .mb-0 }

```markdown
# H1 - heading
{: .mt-4 .mb-0 }
```
{: file="Cú pháp"}

## H2 - heading
{: data-toc-skip='' .mt-4 .mb-0 }

```markdown
## H2 - heading
{: data-toc-skip='' .mt-4 .mb-0 }
```
{: file="Cú pháp"}

### H3 - heading
{: data-toc-skip='' .mt-4 .mb-0 }

```markdown
### H3 - heading
{: data-toc-skip='' .mt-4 .mb-0 }
```
{: file="Cú pháp"}

#### H4 - heading
{: data-toc-skip='' .mt-4 }

```markdown
#### H4 - heading
{: data-toc-skip='' .mt-4 }
```
{: file="Cú pháp"}

## Paragraph

Quisque egestas convallis ipsum, ut sollicitudin risus tincidunt a. Maecenas interdum malesuada egestas. Duis consectetur porta risus, sit amet vulputate urna facilisis ac. Phasellus semper dui non purus ultrices sodales. Aliquam ante lorem, ornare a feugiat ac, finibus nec mauris. Vivamus ut tristique nisi. Sed vel leo vulputate, efficitur risus non, posuere mi. Nullam tincidunt bibendum rutrum. Proin commodo ornare sapien. Vivamus interdum diam sed sapien blandit, sit amet aliquam risus mattis. Nullam arcu turpis, mollis quis laoreet at, placerat id nibh. Suspendisse venenatis eros eros.

```markdown
Quisque egestas convallis ipsum, ut sollicitudin risus tincidunt a. Maecenas interdum malesuada egestas. Duis consectetur porta risus, sit amet vulputate urna facilisis ac. Phasellus semper dui non purus ultrices sodales. Aliquam ante lorem, ornare a feugiat ac, finibus nec mauris. Vivamus ut tristique nisi. Sed vel leo vulputate, efficitur risus non, posuere mi. Nullam tincidunt bibendum rutrum. Proin commodo ornare sapien. Vivamus interdum diam sed sapien blandit, sit amet aliquam risus mattis. Nullam arcu turpis, mollis quis laoreet at, placerat id nibh. Suspendisse venenatis eros eros.
```
{: file="Cú pháp"}

## Lists

### Ordered list

1. Firstly
2. Secondly
3. Thirdly

```markdown
1. Firstly
2. Secondly
3. Thirdly
```
{: file="Cú pháp"}

### Unordered list

- Chapter
  + Section
    * Paragraph

```markdown
- Chapter
  + Section
    * Paragraph
```
{: file="Cú pháp"}

### ToDo list

- [ ] Job
  + [x] Step 1
  + [x] Step 2
  + [ ] Step 3

```markdown
- [ ] Job
  + [x] Step 1
  + [x] Step 2
  + [ ] Step 3
```
{: file="Cú pháp"}

### Description list

Sun
: the star around which the earth orbits

Moon
: the natural satellite of the earth, visible by reflected light from the sun

```markdown
Sun
: the star around which the earth orbits

Moon
: the natural satellite of the earth, visible by reflected light from the sun
```
{: file="Cú pháp"}

## Block Quote

> This line shows the _block quote_.

```markdown
> This line shows the _block quote_.
```
{: file="Cú pháp"}

## Prompts

> An example showing the `tip` type prompt.
{: .prompt-tip }

```markdown
> An example showing the `tip` type prompt.
{: .prompt-tip }
```
{: file="Cú pháp"}

> An example showing the `info` type prompt.
{: .prompt-info }

```markdown
> An example showing the `info` type prompt.
{: .prompt-info }
```
{: file="Cú pháp"}

> An example showing the `warning` type prompt.
{: .prompt-warning }

```markdown
> An example showing the `warning` type prompt.
{: .prompt-warning }
```
{: file="Cú pháp"}

> An example showing the `danger` type prompt.
{: .prompt-danger }

```markdown
> An example showing the `danger` type prompt.
{: .prompt-danger }
```
{: file="Cú pháp"}

## Tables

| Company                      | Contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |

```markdown
| Company                      | Contact          | Country |
|:-----------------------------|:-----------------|--------:|
| Alfreds Futterkiste          | Maria Anders     | Germany |
| Island Trading               | Helen Bennett    | UK      |
| Magazzini Alimentari Riuniti | Giovanni Rovelli | Italy   |
```
{: file="Cú pháp"}

## Links

<http://127.0.0.1:4000>

```markdown
<http://127.0.0.1:4000>
```
{: file="Cú pháp"}

## Footnote

Click the hook will locate the footnote[^footnote], and here is another footnote[^fn-nth-2].

```markdown
Click the hook will locate the footnote[^footnote], and here is another footnote[^fn-nth-2].
```
{: file="Cú pháp"}

## Inline code

This is an example of `Inline Code`.

```markdown
This is an example of `Inline Code`.
```
{: file="Cú pháp"}

## Filepath

Here is the `/path/to/the/file.extend`{: .filepath}.

```markdown
Here is the `/path/to/the/file.extend`{: .filepath}.
```
{: file="Cú pháp"}

## Code blocks

### Common

```
This is a common code snippet, without syntax highlight and line number.
```

Cú pháp
> <pre>
> ```
> This is a common code snippet, without syntax highlight and line number.
> ```
> </pre>

### Specific Language

```bash
if [ $? -ne 0 ]; then
  echo "The command was not successful.";
  #do the needful / exit
fi;
```

Cú pháp
> <pre>
> ```bash
> if [ $? -ne 0 ]; then
>   echo "The command was not successful.";
>   #do the needful / exit
> fi;
> ```
> </pre>

### Specific filename

```sass
@import
  "colors/light-typography",
  "colors/dark-typography";
```
{: file='_sass/jekyll-theme-chirpy.scss'}

Cú pháp
> <pre>
> ```sass
> @import
>   "colors/light-typography",
>   "colors/dark-typography";
> ```
> {: file='_sass/jekyll-theme-chirpy.scss'}
> </pre>

## Mathematics

The mathematics powered by [**MathJax**](https://www.mathjax.org/):

$$ \sum_{n=1}^\infty 1/n^2 = \frac{\pi^2}{6} $$

When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$

```md
$$ \sum_{n=1}^\infty 1/n^2 = \frac{\pi^2}{6} $$

When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are

$$ x = {-b \pm \sqrt{b^2-4ac} \over 2a} $$
```
{: file="Cú pháp"}

## Mermaid SVG



```mermaid
 gantt
  title  Adding GANTT diagram functionality to mermaid
  apple :a, 2017-07-20, 1w
  banana :crit, b, 2017-07-23, 1d
  cherry :active, c, after b a, 1d
```

Cú pháp
> <pre>
> ```mermaid
>  gantt
>   title  Adding GANTT diagram functionality to mermaid
>   apple :a, 2017-07-20, 1w
>   banana :crit, b, 2017-07-23, 1d
>   cherry :active, c, after b a, 1d
> ```
> </pre>



## Images

### Default (with caption)

![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" }
_Full screen width and center alignment_

```md
![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" }
_Full screen width and center alignment_
```
{: file="Cú pháp"}

### Left aligned

![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" .w-75 .normal}

### Float to left

![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" .w-50 .left}
Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra, sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula condimentum.

```md
![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" .w-50 .left}
Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra, sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula condimentum.
```
{: file="Cú pháp"}

### Float to right

![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" .w-50 .right}
Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra, sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula condimentum.

```md
![Desktop View](/assets/img/text-and-typography/mockup.png){: width="972" height="589" .w-50 .right}
Praesent maximus aliquam sapien. Sed vel neque in dolor pulvinar auctor. Maecenas pharetra, sem sit amet interdum posuere, tellus lacus eleifend magna, ac lobortis felis ipsum id sapien. Proin ornare rutrum metus, ac convallis diam volutpat sit amet. Phasellus volutpat, elit sit amet tincidunt mollis, felis mi scelerisque mauris, ut facilisis leo magna accumsan sapien. In rutrum vehicula nisl eget tempor. Nullam maximus ullamcorper libero non maximus. Integer ultricies velit id convallis varius. Praesent eu nisl eu urna finibus ultrices id nec ex. Mauris ac mattis quam. Fusce aliquam est nec sapien bibendum, vitae malesuada ligula condimentum.
```
{: file="Cú pháp"}

### Dark/Light mode & Shadow

The image below will toggle dark/light mode based on theme preference, notice it has shadows.

![light mode only](/assets/img/text-and-typography/devtools-light.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/img/text-and-typography/devtools-dark.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }

```md
![light mode only](/assets/img/text-and-typography/devtools-light.png){: .light .w-75 .shadow .rounded-10 w='1212' h='668' }
![dark mode only](/assets/img/text-and-typography/devtools-dark.png){: .dark .w-75 .shadow .rounded-10 w='1212' h='668' }
```
{: file="Cú pháp"}

## Video

{% include embed/youtube.html id='Balreaj8Yqs' %}

```md
{% raw %}{% include embed/youtube.html id='Balreaj8Yqs' %}{% endraw %}
```
{: file="Cú pháp"}

## Reverse Footnote

[^footnote]: The footnote source
[^fn-nth-2]: The 2nd footnote source

```md
[^footnote]: The footnote source
[^fn-nth-2]: The 2nd footnote source
```
{: file="Cú pháp"}