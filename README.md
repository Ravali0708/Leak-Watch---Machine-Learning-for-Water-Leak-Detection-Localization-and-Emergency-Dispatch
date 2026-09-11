**LeakWatch**
****Machine Learning for Water-Leak Detection, Localization, and Emergency Dispatch
****
Hi, this is my MS Data Science project. I wanted to explain it here in simple words so anyone reading my repository understands what I am building, why, and how it works.

**##What is this project?**

LeakWatch is a program that looks at water-pressure readings from a few sensors placed on a water network and figures out three things:

Is there a leak? (detection)
Where is the leak? (localization)
Which repair crew should be sent, and by what route? (dispatch)

So the simple idea is: sensor readings go in, and a "there is a leak near here, send this crew" decision comes out. It runs as a pipeline, meaning the data passes through a few steps and each step does one job.
**##Why I picked this project**

Cities lose a lot of their clean water — around 30 to 50 percent — through leaks in underground pipes that no one can see. For example, Oklahoma City had over 1,100 water-main breaks last year, mostly in old iron pipes stressed by the clay soil and cold weather. Because the pipes are underground, a leak is usually noticed only after water reaches the street. My project is about catching these leaks earlier and sending crews to the right place faster.
**##How I get the data**

There is no free public dataset of real, labeled water leaks, because water companies don't share that kind of data. So, like researchers in this area do, **I generate my own data by simulation.**

I use a free water simulator called EPANET, which I control from Python using a tool called WNTR.
I load a standard water network called Net3, and I add a leak myself — I choose the location, the size, and the time.
The simulator then calculates the pressure at each sensor over time.
Because I placed the leak myself, I always know the true answer, which is what lets me measure how accurate my models are.

**Later I plan to test my trained models on a real public benchmark called BattLeDIM (real sensor data with known leaks) to show the method also works on real-world data.**

**##How the project works (step by step)**
**1. Generate data** — simulate many leaks and save a labeled dataset.
**2. Feature engineering** — turn the raw pressures into the residual (the difference between the normal expected pressure and the actual reading). This removes the daily rise and fall of water use, so a leak stands out. Residual = expected-normal − actual.
**3. Detection model** — train a model to tell leak from no-leak, and test it on leaks it never saw.
**4. Localization model** — train a second model to find which node the leak is at, from the pattern of pressure drops.
**5. Dispatch**— turn the network into a graph and use shortest-path routing to send the nearest crew.
**6. Evaluate** — compare against a simple baseline, and check how fast and how accurately it works (and how it holds up with sensor noise).

**##Tools I am using**
**Python**— the main language
**WNTR + EPANET** — to simulate the network and make the data
**pandas / NumPy** — to handle the data
**scikit-learn** — to build the detection and localization models
**NetworkX** — for the network graph and the shortest-path dispatch
**Matplotlib** — for the charts
**Google Colab** — where I write and run everything
**GitHub** — to store the project


**##Project structure**
leakwatch/
├── README.md                 <- this file (project overview)
├── notebooks/                <- my Colab notebooks (the main work)
│   └── MS_Project.ipynb
├── data/                     <- the sensor datasets I generate (CSV files)
├── results/                  <- charts and result images
└── src/                      <- helper scripts (added as the project grows)

**##What is my own work**
I did not invent the simulator or the algorithms — those are tools I use. My own contribution is: generating my own labeled dataset, engineering the residual feature, building and training the detection and localization models, adding the crew-dispatch step, and testing everything honestly against a baseline.

**##Honest notes**
This is a project built on simulated data, which is the standard way to do research in this area. I plan to validate on the real BattLeDIM benchmark.
With only a few sensors, I can find the leak's area rather than always the exact pipe.
I am building this step by step, so some parts above are still in progress.

**##References**
WNTR documentation — https://usepa.github.io/WNTR/
EPANET (U.S. EPA) — https://www.epa.gov/water-research/epanet
BattLeDIM — https://battledim.ucy.ac.cy/ | dataset: https://zenodo.org/records/4017659
LeakDB — https://github.com/KIOS-Research/LeakDB
