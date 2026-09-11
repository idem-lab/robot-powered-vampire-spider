# robot-powered-vampire-spider
even scarier than it sounds!
-----------------------------

This is a toy repository to demonstrate an agentic AI workflow in a stereotypical(?) malaria model.

All R code is Claude-written and human-reviewed. This repo is to be built live. This `REAMDE.md` is human-written with AI help in formatting maths

### The science

The cute critter below is *Evarcha culicivora* or a **Vampire Jumping Spider** found around Lake Victoria. It has the unique feeding strategy of specifically hunting female *Anopheles* mosquitoes that have recently had a blood meal, thus the name.

![Evarcha culicivora](https://earthlingnature.wordpress.com/wp-content/uploads/2020/10/image.png)

Imagine if we managed to breed these tiny spiders into mega super powerful predators of *Anopheles* mosquitoes (and try not to imagine the collateral consequences), could they be useful as a vector control tool? In this repo we build a simple simulation experiment of infection dynamics crossed with predator-prey dynamics.

Take the standard Ross-MacDonald from the Anderson & May book:

$$
\begin{aligned}
\frac{dx}{dt} &= \frac{M}{H}abz(1-x) - rx \\
\frac{dz}{dt} &= acx(1-z) - gz
\end{aligned}
$$

where we have
| Symbol | Meaning | Units |
|---|---|---|
| $x(t)$ | human infection prevalence | — |
| $z(t)$ | mosquito infectious prevalence | — |
| $H$ | human population size | — |
| $M(t)$ | mosquito population size | — |
| $a$ | human biting rate per mosquito | day⁻¹ |
| $b$ | transmission efficiency, mosquito $\to$ human | — |
| $c$ | transmission efficiency, human $\to$ mosquito | — |
| $r$ | human recovery rate | day⁻¹ |
| $g$ | mosquito mortality rate | day⁻¹ |

consider $H$, $a$, $b$, $c$, $r$, $g$ all fixed, and consider that $M(t)$ changes over time due to predation by them vampire spiders whose population is $S(t)$. Now we also have a Lotka-Volterra model for predator-prey:

$$
\begin{aligned}
\frac{dM}{dt} &= (\lambda - g)M - \beta M S \\
\frac{dS}{dt} &= \varepsilon \beta M S - \mu S
\end{aligned}
$$

where we have:
| Symbol | Meaning | Units |
|---|---|---|
| $S(t)$ | spider population | — |
| $\lambda$ | mosquito birth rate | day⁻¹ |
| $\beta$ | predation rate per predator per mosquito | day⁻¹ |
| $\varepsilon$ | conversion efficiency, mosquitoes eaten → new spiders | — |
| $\mu$ | spider mortality rate | day⁻¹ |

Now we can ask some science questions: under what parameter regime and initial conditions do vampire spiders help reduce human malaria prevalence, and by how much? This system of differential equations may well have analytical solutions but that's beyond my skills, so we'll use some discrete time simulations to explore these.

### Initiation rite:

August to summon Claude and bind its power to do the following:

- build basic scaffolding (one-off task):
  - `analysis.R` - main analysis script that lives in project root
  - `/R` - function definitions 
  - `/aux` - light reading for Claude
  - `/outputs` - stuff made by `analysis.R`
- initialise CLAUDE.md documentation and keep it up to date

### Commandments

- Claude to generally follow coding style and plotting preference in the example R script inside `/aux` - the script only exists as reading material for Claude and is not used in this work.
- All output figures, Shiny apps, markdown files etc. are to be sized for projector display and use colour-weakness-friendly palettes, use less white space and bigger font as a general rule, but use your good senses too.
- When given a task, Claude is to first create an issue documenting the task, then to make a branch to do the work. Once the work is deemed done, Claude is to make a Pull Request for human review.
- Claude to build simulation in discrete time and use base R functions where possible, do not use ODE solvers.
- At all stages, keep commit messages, PR requests, and general documentations succinct and human reviewable.
- Claude can commit, pull, push, flag merging conflicts, and suggest edits to `.gitignore`, but merging PR is human job.
- When making a PR, quote the human prompt behind key decisions.
