## Project Overview & Problem Statement

**Client:** *PowerGrid Central* – a regional electricity provider responsible for maintaining a stable, 24/7 electricity supply to residential, commercial, and industrial sectors.

**Problem:**
PowerGrid Central currently forecasts electricity demand using simple historical averages. While easy to implement, this method often fails to capture non-linear and abrupt demand changes—especially during extreme weather events or behavioral shifts. This leads to:

- Over-generation: Wasted fuel and operational costs.
- Under-generation: Costly emergency power purchases and risk of brownouts.
- Poor outage planning: Maintenance scheduling becomes inefficient and risky.

### Project Goal
Develop a machine learning-based time series forecasting model to:
- Enable smarter generation scheduling aligned with actual demand.
- Reduce reliance on emergency purchases and lower operational costs.
- Improve outage and maintenance planning.
- Avoid over- and under-generation to enhance financial efficiency.
- Provide insights into key demand drivers (time, seasonality, temperature).

![Dashboard Preview](images/churn.gif)

## Setup and Data Loading

**Goal:** Initialize the environment, load the dataset, and inspect for data quality issues.

### Steps:
- Import essential libraries: \`pandas\`, \`numpy\`, \`matplotlib\`, \`seaborn\`, \`sklearn\`.
- Load \`AEP_hourly.csv\` into a DataFrame.
- Perform initial inspection:
  - \`.head()\`, \`.info()\`, \`.describe()\` to explore structure.
  - \`.isnull().sum()\` and \`.duplicated()\` to identify cleaning needs.

## Exploratory Data Analysis (EDA)

**Objective:** Discover temporal patterns like trends, seasonality, and anomalies.

### a. Datetime Preprocessing
- Convert and extract features: \`hour\`, \`day\`, \`weekday\`, \`month\`, \`year\`.

### b. Target Variable Overview (\`MW_Demand\`)
- Plot full time series and demand distribution.
- Spot skewness, spikes, and outliers.

### c. Seasonality Patterns
- Create time-based features for exploration.
- Analyze:
  - Yearly demand shifts.
  - Weekly differences (weekdays vs weekends).
  - Daily/Hourly consumption cycles.

**Outcome:** Clear insight into demand patterns to guide feature engineering and model selection.

## Data Preparation and Feature Engineering

**Objective:** Transform raw time series into a model-ready dataset.

### a. Feature Engineering
Engineered features:
- Time-based: Hour, Day of Week, Month, Year
- Contextual: Season (Winter, Spring, Summer, Fall)
- Aggregated: Daily average demand, optional rolling averages

### b. Feature Preparation and Encoding
- Apply One-Hot Encoding to categorical variables like season and day_of_week.
- Ensure model compatibility and avoid ordinal bias.

**Outcome:** A rich, structured dataset ready for model training.

## Model Training and Evaluation

**Objective:** Train and evaluate forecasting models on future unseen data.

### a. Define Features and Target
- Target (\`y\`): \`MW_Demand\`
- Features (\`X\`): Time and contextual variables

### b. Time-Based Train-Test Split
- Train: Data before 2015
- Test: Data from 2015 onward

### c. Model Training and Comparison
Models:
- Random Forest Regressor – strong baseline, handles non-linearities well
- XGBoost Regressor – gradient boosting model with high performance

### d. Final Evaluation and Model Selection
Metrics:
- R Squared(R2)
- Mean Squared Error
- Root Mean Squared Error(RMSE)
- Mean Absolute Error(MAE)
- Mean Absoulte Percentage Error(MAPE)

The model with the lowest test error will be selected.

**Outcome:** A robust and generalizable model for forecasting energy demand.

## Conclusion and Final Assessment

### a. Summary of Model Performance
After comparing both models on the same test set:
- XGBoost Regressor achieved higher R², lower MSE, and better MAPE on unseen data.
- Random Forest slightly overfitted and had a larger error gap between train and test.

### b. Model Strengths and Limitations
- XGBoost: Excellent at generalizing unseen demand patterns.
- Random Forest: Easier to interpret but prone to overfitting in this case.

### c. Final Recommendation and Business Impact
- Deploy XGBoost for future energy forecasting due to superior generalization.
- Implement monitoring for model drift and periodic retraining.

**Outcome:**
A high-performing forecasting solution ready for deployment. It supports better operational decisions, minimizes cost inefficiencies, and increases the stability of the power grid.
`
  },
  {
    id: 3,
    isFeatured: true,
    title: 'Ames Housing Price Prediction',
    summary: 'A data-driven regression model to predict home prices for a real estate agency, replacing agent intuition with consistent, justifiable estimates.',
    gifUrl: '/images/house_pricing.gif',
    tags: ['Python', 'Regression', 'XGBoost', 'Feature Engineering', 'Power BI'],
    githubUrl: 'https://github.com/Fretch-troy1001/housing-price-prediction',
    liveLink: null,
    detailedContent: `
## Project Goal
The project answers two key questions:
1. **Can we build a regression model that predicts house prices with accuracy and consistency?**
2. **Which features most strongly influence a home’s sale price?**

## Setup and Data Loading
The first phase focused on preparing the programming environment and getting familiar with the dataset.
- Imported essential libraries: \`pandas\`, \`numpy\`, \`matplotlib\`, and \`seaborn\`
- Loaded the \`train.csv\` dataset into a pandas DataFrame
- Used \`.head()\`, \`.info()\`, \`.describe()\`, and \`.isnull().sum()\` to:
  - Understand the structure and data types
  - Spot early signs of missing data
  - Get a feel for the numerical distributions
This initial inspection laid the groundwork for data cleaning and EDA.

## Exploratory Data Analysis (EDA)
The goal of this phase was to identify patterns, test assumptions, and uncover the most predictive features.
- **Analyzed the Target Variable:** SalePrice was heavily right skewed. We noted this early for later transformation.
- **Identified Top Numerical Features:** Using a correlation matrix, we ranked numerical variables based on their linear relationship with SalePrice.
- **Categorical Impact:** Calculated median SalePrice per category for fields like \`Neighborhood\`, \`KitchenQual\`, and \`GarageFinish\`.
- **Visual Exploration:** Created scatter plots and boxplots to confirm relationships, assess linearity, and detect significant outliers.
The insights from this phase directly informed our feature engineering and modeling strategies.

## Data Preparation and Feature Engineering
With our raw data understood and cleaned, we shifted to preparing it for modeling.
### a. Feature Engineering
We created new variables to capture meaningful patterns:
- **\`TotalSF\`**: Combined basement, first, and second floor areas into one measure of total square footage.
- **\`HouseAge\`**: Calculated as the difference between \`YrSold\` and \`YearBuilt\`.
We also reassessed outliers using correlation and distribution plots.
### b. Feature Preparation & Encoding
To make all features model ready:
- **Ordinal Encoding**: Applied to rank based categories like \`ExterQual\` and \`GarageCond\`.
- **One Hot Encoding**: Used for nominal variables like \`Neighborhood\`, ensuring models don’t misinterpret arbitrary numeric mappings.
- **Dropped \`Id\`** as it had no predictive value.
### c. Target Variable Transformation
To address the skewed distribution of \`SalePrice\`, we applied a log transformation (\`np.log1p\`). This normalization helped meet assumptions for linear regression and improved model stability.

## Model Training and Evaluation
We evaluated three regression models on the cleaned and engineered dataset:
1. **Linear Regression** – served as our baseline model.
2. **Random Forest** – introduced non linear modeling power.
3. **XGBoost** – our final, tuned model using \`GridSearchCV\`.
We split the data into training and test sets using \`train_test_split\`, ensuring unbiased performance measurement. XGBoost was ultimately selected for its balance of accuracy, interpretability, and generalization.

## Final Results
- **Best Model:** Tuned XGBoost
- **R² Score on test set:** ~91% (92.5% when we undo the logistic transformation)
- **RMSE (test data):** ~$20,350
### Most Influential Features: 
Based on model importance and earlier correlation analysis:
- \`OverallQual\`
- \`TotalSF\` 
- \`KitchenQual\`
- \`GarageFinish\`
- \`GarageCars\`

## Business Impact
The model provides Ames Real Estate agents with a reliable pricing tool, replacing guesswork with data backed estimates. It also offers transparency like helping agents explain that overall quality influence its value, and where investments (like kitchen upgrades) are likely to pay off. 
Visualizations from PowerBI is also implemented to provide more insights to the model and its limitations. And how to use each features to have the most accurate pricing.

## Technologies Used
- Python
- pandas & numpy
- matplotlib & seaborn
- scikit-learn
- XGBoost
- JupyterLab
- Power BI
`
  },
  {
    id: 2,
    isFeatured: false,
    title: 'Customer Churn Prediction Model',
    summary: 'A machine learning model that predicts customer churn with 88% accuracy, enabling proactive retention campaigns and saving an estimated $1.5M annually.',
    gifUrl: '/images/project-churn.gif',
    tags: ['Machine Learning', 'Python', 'Scikit-learn', 'Feature Engineering'],
    githubUrl: 'https://github.com/your-username/your-churn-project',
    liveLink: null,
    detailedContent: `
### The Challenge
A major telecom company was experiencing high customer churn but lacked the tools to identify which customers were most likely to leave. They needed a proactive way to retain valuable clients before they made the decision to switch providers.

### My Solution
I developed an end-to-end machine learning pipeline to address this problem.
- **Feature Engineering:** I extracted and engineered over 50 features from customer usage data, demographic information, and historical service logs.
- **Model Development:** Using Python and Scikit-learn, I trained and rigorously evaluated several classification models, including Logistic Regression, Random Forest, and Gradient Boosting.
- **Deployment:** The final Gradient Boosting model was selected for its high accuracy and interpretability. It was then integrated into a system that flags at-risk customers daily, feeding this information directly into the marketing team's CRM for targeted retention campaigns.

### Business Impact
The model predicts customer churn with **88% accuracy**. This has allowed the marketing team to focus their retention efforts effectively, leading to a **12% reduction in churn** within the first quarter of implementation and an estimated annual savings of **$1.5M**.
`
  },
];

// --- Sliding Text Component for Homepage ---
const SlidingText = () => {
    const content = [
        {
            type: 'quote',
            text: '&ldquo;Every person who has ever achieved something meaningful in their life began with a single decision...<br/>The decision to <span class="text-blue-400 font-bold tracking-wider uppercase">BEGIN</span>.&rdquo;'
        },
        {
            type: 'intro',
            text: "That mindset changed everything for me. After years of working as a turbine engineer, I made the decision to start over, not because I had to, but because I believed I could build something more impactful with data. That moment of commitment led me into analytics, late-night learning sessions, and the pursuit of insights that truly matter."
        },
        {
            type: 'intro',
            text: "Today, I apply the same engineering discipline to solving problems with data. I focus on transforming raw information into clear narratives and predictive models, always bridging technical complexity and business value. Whether I’m writing SQL, building dashboards in Power BI, coding in Python, or validating machine learning forecasts, I bring structure, clarity, and a drive to deliver meaningful results."
        },
        {
            type: 'intro',
            text: "This journey has required sacrifice, consistency, and deep focus. But it has also proven that growth doesn't depend on perfect conditions. It begins with a decision, followed by relentless action. I now dedicate myself to building data-driven solutions that help teams think clearly, act strategically, and move forward with confidence."
        }
    ];
    const [currentIndex, setCurrentIndex] = useState(0);

    useEffect(() => {
        const duration = content[currentIndex].type === 'quote' ? 8000 : 12000;
        const timer = setInterval(() => {
            setCurrentIndex(prevIndex => (prevIndex + 1) % content.length);
        }, duration);
        return () => clearInterval(timer);
    }, [currentIndex, content.length]);

    return (
        <div className="relative h-64 md:h-56">
            {content.map((item, index) => {
                const isQuote = item.type === 'quote';
                const containerJustify = isQuote ? 'justify-center' : 'justify-start';
                const styleClasses = isQuote 
                    ? "text-xl md:text-2xl font-serif italic text-slate-300 text-center"
                    : "text-base md:text-lg text-slate-300 leading-loose text-left";

                return (
                    <div 
                        key={index}
                        className={`absolute inset-0 transition-opacity duration-1000 ease-in-out flex items-center ${containerJustify} ${
                            index === currentIndex ? 'opacity-100' : 'opacity-0'
                        }`}
                    >
                        <p className={styleClasses} dangerouslySetInnerHTML={{ __html: item.text }} />
                    </div>
                );
            })}
            <div className="absolute -bottom-4 left-1/2 -translate-x-1/2 flex gap-2">
                {content.map((_, index) => (
                    <button 
                        key={index}
                        onClick={() => setCurrentIndex(index)}
                        className={`w-2.5 h-2.5 rounded-full transition-colors ${
                            index === currentIndex ? 'bg-blue-400' : 'bg-slate-600 hover:bg-slate-500'
                        }`}
                        aria-label={`Go to slide ${index + 1}`}
                    />
                ))}
            </div>
        </div>
    );
};

// --- Featured Projects Component with Swipe Transition ---
const FeaturedProjects = ({ viewProject }) => {
    const featured = projectsData.filter(p => p.isFeatured);
    const [currentIndex, setCurrentIndex] = useState(0);
    const [isTransitioning, setIsTransitioning] = useState(false);
    const project = featured[currentIndex];

    // Automatic slideshow effect
    useEffect(() => {
        if (featured.length <= 1) return;

        const timer = setInterval(() => {
            setIsTransitioning(true);
            // Wait for the exit animation to complete before changing the project
            setTimeout(() => {
                setCurrentIndex((prev) => (prev + 1) % featured.length);
                setIsTransitioning(false);
            }, 1000); // This duration should match the transition duration
        }, 12000); // Time per slide, matching the longest intro text

        return () => clearInterval(timer);
    }, [featured.length]);

    if (!project) return null;

    return (
        <div>
            <h2 className="text-3xl font-bold text-center text-white mb-12">Featured Projects</h2>
            <div className="relative bg-slate-800/50 rounded-xl shadow-lg overflow-hidden p-8 md:p-12 h-[28rem] md:h-[26rem]">
                <div 
                    key={project.id} // The key change triggers the re-render for the animation
                    className={`
                        grid md:grid-cols-2 gap-8 md:gap-12 items-center
                        transition-all duration-1000 ease-in-out
                        ${isTransitioning ? 'opacity-0 transform -translate-x-10' : 'opacity-100 transform translate-x-0'}
                    `}
                >
                    {/* Left Panel: Project Details */}
                    <div>
                        <h3 className="text-2xl font-bold text-white">{project.title}</h3>
                        <p className="mt-4 text-slate-400 h-24">{project.summary}</p>
                        <div className="mt-4 flex flex-wrap gap-2">
                            {project.tags.map(tag => (
                                <span key={tag} className="text-xs font-semibold bg-slate-700 text-slate-300 px-2.5 py-1 rounded-full">{tag}</span>
                            ))}
                        </div>
                        <button 
                            onClick={() => viewProject(project)}
                            className="inline-flex items-center mt-6 text-blue-400 group"
                        >
                            View Project Details <ArrowRight className="ml-2 h-4 w-4 transition-transform group-hover:translate-x-1" />
                        </button>
                    </div>
                    {/* Right Panel: Project GIF */}
                    <div className="w-full h-64 md:h-80 rounded-lg overflow-hidden">
                        <img 
                            className="w-full h-full object-cover" 
                            src={project.gifUrl} 
                            alt={project.title} 
                            onError={(e) => { e.target.onerror = null; e.target.src = 'https://placehold.co/600x400/1E293B/94A3B8?text=Project+GIF'; }}
                        />
                    </div>
                </div>
            </div>
        </div>
    );
};


// 1. Home Page (Updated to use FeaturedProjects component)
const HomePage = ({ viewProject }) => {
  const fadeInProps = useFadeIn();

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16 md:py-24">
      <div {...fadeInProps}>
        <div className="grid md:grid-cols-3 gap-12 items-center mb-24">
          <div className="md:col-span-2">
            <h1 className="text-4xl md:text-5xl font-extrabold text-white leading-tight mb-8">
              From <span className="text-blue-400">Turbines</span> to <span className="text-blue-400">Trends</span>
            </h1>
            <SlidingText />
          </div>
          <div className="flex justify-center items-center">
            <img 
              src="/images/profile_pic.jpg"
              alt="Fretch Royette Ybañez"
              className="w-48 h-48 md:w-64 md:h-64 rounded-full object-cover shadow-lg border-4 border-slate-700"
              onError={(e) => { e.target.onerror = null; e.target.src = 'https://placehold.co/256x256/1E293B/94A3B8?text=F.R.Y.'; }}
            />
          </div>
        </div>
        
        <FeaturedProjects viewProject={viewProject} />

      </div>
    </div>
  );
};


// 2. Projects List Page
const ProjectsPage = ({ viewProject }) => {
  const fadeInProps = useFadeIn();

  const tagIconMap = {
    'All': <Layers size={14} className="mr-1.5" />,
    'Python': <CodeXml size={14} className="mr-1.5" />,
    'Power BI': <BarChartBig size={14} className="mr-1.5" />,
    'Machine Learning': <BrainCircuit size={14} className="mr-1.5" />,
    'SQL': <Database size={14} className="mr-1.5" />,
    'Time Series': <TrendingUp size={14} className="mr-1.5" />,
    'XGBoost': <BrainCircuit size={14} className="mr-1.5" />,
    'Feature Engineering': <Blocks size={14} className="mr-1.5" />,
    'Scikit-learn': <CodeXml size={14} className="mr-1.5" />,
    'Regression': <LineChart size={14} className="mr-1.5" />,
  };

  const allTags = ['All', ...new Set(projectsData.flatMap(p => p.tags))];
  const [activeFilter, setActiveFilter] = useState('All');

  const filteredProjects = activeFilter === 'All' 
    ? projectsData 
    : projectsData.filter(p => p.tags.includes(activeFilter));

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
      <div {...fadeInProps}>
        <h2 className="text-3xl font-bold text-center text-white flex items-center justify-center gap-x-3">
          <Layers size={30} className="text-blue-400" />
          All Projects
        </h2>

        <div className="flex justify-center flex-wrap gap-2 mt-8">
          {allTags.map(tag => (
            <button 
              key={tag} 
              onClick={() => setActiveFilter(tag)} 
              className={`inline-flex items-center justify-center px-4 py-2 text-sm font-medium rounded-full transition-colors ${
                activeFilter === tag 
                  ? 'bg-blue-600 text-white' 
                  : 'bg-slate-700 hover:bg-slate-600'
              }`}
            >
              {tagIconMap[tag] || <Asterisk size={14} className="mr-1.5" />}
              {tag}
            </button>
          ))}
        </div>

        <div className="mt-12 grid md:grid-cols-2 lg:grid-cols-3 gap-8">
          {filteredProjects.map(project => (
            <div 
              key={project.id}
              className="bg-slate-800/50 rounded-xl shadow-lg overflow-hidden cursor-pointer group hover:bg-slate-800 transition-all duration-300 p-6 flex flex-col"
              onClick={() => viewProject(project)}
            >
              <h3 className="text-xl font-bold text-white group-hover:text-blue-400 transition-colors">{project.title}</h3>
              <p className="mt-2 text-slate-400 text-sm flex-grow">{project.summary}</p>
              <div className="mt-4 flex flex-wrap gap-2">
                {project.tags.map(tag => (
                  <span key={tag} className="inline-flex items-center text-xs font-semibold bg-slate-700 text-slate-300 px-2.5 py-1 rounded-full">
                    {tagIconMap[tag] || <Asterisk size={12} className="mr-1" />}
                    {tag}
                  </span>
                ))}
              </div>
              <div className="inline-flex items-center mt-6 text-blue-400 text-sm font-semibold">
                  View Details <ArrowRight className="ml-2 h-4 w-4 transition-transform group-hover:translate-x-1" />
              </div>
            </div>
          ))}
        </div>
      </div>
    </div>
  );
};

// 3. Resume Page
const ResumePage = () => {
  const fadeInProps = useFadeIn();
  const skills = [
    { name: 'Python (Pandas, Scikit-learn)', level: '90%' },
    { name: 'SQL & Database Management', level: '90%' },
    { name: 'Machine Learning & Modeling', level: '85%' },
    { name: 'Power BI / Tableau', level: '85%' },
    { name: 'Cloud (AWS, GCP)', level: '70%' },
    { name: 'Data Storytelling & Communication', level: '95%' },
  ];

  const skillIconMap = {
    'Python (Pandas, Scikit-learn)': <CodeXml size={18} className="text-blue-400" />,
    'SQL & Database Management': <Database size={18} className="text-blue-400" />,
    'Machine Learning & Modeling': <BrainCircuit size={18} className="text-blue-400" />,
    'Power BI / Tableau': <BarChartBig size={18} className="text-blue-400" />,
    'Cloud (AWS, GCP)': <Cloud size={18} className="text-blue-400" />,
    'Data Storytelling & Communication': <Presentation size={18} className="text-blue-400" />,
  };

  const experiences = [
    { role: 'Data Scientist / Analyst (Freelance)', company: 'Various Clients', period: '2023 - Present', icon: <LineChart className="h-5 w-5 text-slate-400" /> },
    { role: 'Senior Mechanical Engineer', company: 'Global Turbine Solutions', period: '2018 - 2023', icon: <Cog className="h-5 w-5 text-slate-400" /> },
    { role: 'Mechanical Engineer', company: 'Energy Corp.', period: '2015 - 2018', icon: <Cog className="h-5 w-5 text-slate-400" /> },
  ];

  return (
    <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
      <div {...fadeInProps}>
        <h2 className="text-3xl font-bold text-center text-white flex items-center justify-center gap-x-3">
            <UserSquare size={30} className="text-blue-400"/>
            My Professional Journey
        </h2>
        <p className="mt-4 max-w-2xl mx-auto text-center text-lg text-slate-400">
          A summary of my skills, experience, and formal qualifications.
        </p>
        
        <div className="text-center mt-8">
            <a href="/FretchRoyetteYbañez_Resume.pdf" download="FretchRoyetteYbañez_Resume.pdf" className="inline-flex items-center px-6 py-3 border border-transparent text-base font-medium rounded-md shadow-sm text-white bg-blue-600 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-blue-500">
                <Download className="mr-3 -ml-1 h-5 w-5" />
                Download Full Resume (PDF)
            </a>
        </div>

        <div className="mt-16 grid md:grid-cols-2 gap-12">
            <div>
                <h3 className="text-2xl font-bold text-white mb-6">Technical & Analytical Skills</h3>
                <div className="space-y-5">
                    {skills.map(skill => (
                        <div key={skill.name}>
                            <div className="flex justify-between items-center mb-1">
                                <span className="flex items-center gap-x-2 text-base font-medium text-slate-300">
                                    {skillIconMap[skill.name] || <Asterisk size={18} className="text-blue-400" />}
                                    {skill.name}
                                </span>
                                <span className="text-sm font-medium text-slate-400">Advanced</span>
                            </div>
                            <div className="w-full bg-slate-700 rounded-full h-2.5">
                                <div className="bg-blue-500 h-2.5 rounded-full" style={{ width: skill.level }}></div>
                            </div>
                        </div>
                    ))}
                </div>
            </div>

            <div>
                <h3 className="text-2xl font-bold text-white mb-6">Career Experience</h3>
                <div className="relative border-l-2 border-slate-700 pl-8 space-y-10">
                    {experiences.map((exp, index) => (
                        <div key={index} className="relative">
                            <div className="absolute -left-[45px] top-1 h-8 w-8 bg-slate-800 rounded-full flex items-center justify-center ring-4 ring-slate-900">
                                {exp.icon}
                            </div>
                            <p className="text-sm text-slate-400">{exp.period}</p>
                            <h4 className="text-lg font-semibold text-slate-200">{exp.role}</h4>
                            <p className="text-slate-400">{exp.company}</p>
                        </div>
                    ))}
                </div>
            </div>
        </div>
      </div>
    </div>
  );
};


// --- Technology List component with Icons ---
const TechnologyList = ({ technologies }) => {
    const iconMap = {
        'python': <CodeXml size={16} className="text-blue-400" />,
        'pandas & numpy': <Database size={16} className="text-blue-400" />,
        'matplotlib & seaborn': <BarChartBig size={16} className="text-blue-400" />,
        'scikit-learn': <BrainCircuit size={16} className="text-blue-400" />,
        'xgboost': <TrendingUp size={16} className="text-blue-400" />,
        'jupyterlab': <PenSquare size={16} className="text-blue-400" />,
        'power bi': <Presentation size={16} className="text-blue-400" />,
    };

    return (
        <div className="grid grid-cols-2 md:grid-cols-3 gap-4 mt-4">
            {technologies.map(tech => (
                <div key={tech} className="flex items-center gap-3 bg-slate-800/50 p-3 rounded-lg">
                    {iconMap[tech.toLowerCase()] || <Asterisk size={16} className="text-blue-400" />}
                    <span className="text-slate-300">{tech}</span>
                </div>
            ))}
        </div>
    );
};

// --- Single Project Detail Page ---
const ProjectDetailPage = ({ project, navigateTo }) => {
  const fadeInProps = useFadeIn();

  const renderContent = (content) => {
    const sections = content.split('## ').slice(1);
    return sections.map((section, index) => {
        const lines = section.split('\n');
        const title = lines[0].trim();
        const body = lines.slice(1);

        if (title === 'Technologies Used') {
            const techList = body.filter(line => line.startsWith('- ')).map(line => line.substring(2).trim());
            return (
                <div key={index}>
                    <h2 className="text-3xl font-bold text-white mt-10 mb-4 border-b border-slate-700 pb-2">{title}</h2>
                    <TechnologyList technologies={techList} />
                </div>
            );
        }

        let htmlContent = '';
        let inList = false;
        body.forEach(line => {
             const trimmedLine = line.trim();
            if (trimmedLine.startsWith('### ')) {
                if (inList) { htmlContent += '</ul>'; inList = false; }
                htmlContent += `<h3 class="text-2xl font-bold text-white mt-8 mb-4">${trimmedLine.substring(4)}</h3>`;
            } else if (trimmedLine.startsWith('- ')) {
                if (!inList) { htmlContent += '<ul class="list-disc pl-5 space-y-2">'; inList = true; }
                htmlContent += `<li class="text-slate-400">${trimmedLine.substring(2)}</li>`;
            } else if(trimmedLine) {
                if (inList) { htmlContent += '</ul>'; inList = false; }
                htmlContent += `<p class="text-slate-400 leading-relaxed my-4">${trimmedLine.replace(/\*\*(.*?)\*\*/g, '<strong>$1</strong>').replace(/\*(.*?)\*/g, '<em>$1</em>')}</p>`;
            }
        });
        if (inList) htmlContent += '</ul>';

        return (
            <div key={index}>
                <h2 className="text-3xl font-bold text-white mt-10 mb-4 border-b border-slate-700 pb-2">{title}</h2>
                <div dangerouslySetInnerHTML={{ __html: htmlContent }} />
            </div>
        );
    });
  };

  return (
    <div className="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 py-16">
      <div {...fadeInProps}>
        <button onClick={() => navigateTo('projects')} className="inline-flex items-center text-blue-400 hover:text-blue-300 mb-8">
          <ArrowLeft className="mr-2 h-4 w-4" />
          Back to All Projects
        </button>
        
        <h1 className="text-4xl font-extrabold text-white">{project.title}</h1>
        <div className="mt-4 flex flex-wrap gap-2">
          {project.tags.map(tag => (
            <span key={tag} className="text-xs font-semibold bg-blue-900/50 text-blue-300 px-2.5 py-1 rounded-full">{tag}</span>
          ))}
        </div>
        
        <div className="mt-8 flex items-center gap-4">
            {project.githubUrl && (
                 <a href={project.githubUrl} target="_blank" rel="noopener noreferrer" className="inline-flex items-center px-4 py-2 border border-slate-600 text-sm font-medium rounded-md text-slate-300 bg-slate-800 hover:bg-slate-700">
                    <Github className="mr-2 h-5 w-5" />
                    View on GitHub
                </a>
            )}
            {project.liveLink && project.liveLink !== '#' && (
                <a href={project.liveLink} target="_blank" rel="noopener noreferrer" className="inline-flex items-center px-4 py-2 border border-transparent text-sm font-medium rounded-md text-white bg-blue-600 hover:bg-blue-700">
                    <ExternalLink className="mr-2 h-5 w-5" />
                    View Live Demo
                </a>
            )}
        </div>

        <img 
          src={project.gifUrl} 
          alt={project.title} 
          className="my-8 rounded-lg shadow-xl w-full"
          onError={(e) => { e.target.onerror = null; e.target.src = 'https://placehold.co/800x450/1E293B/94A3B8?text=Project+Visual'; }}
        />
        
        <div className="prose prose-invert max-w-none">
            {renderContent(project.detailedContent)}
        </div>
      </div>
    </div>
  );
};

// --- Placeholder Pages ---
const BlogPage = () => {
    const fadeInProps = useFadeIn();
    return (
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16" {...fadeInProps}>
            <div className="text-center py-24 bg-slate-800/50 rounded-lg">
                <PenSquare size={48} className="mx-auto text-blue-400" />
                <h2 className="mt-6 text-3xl font-bold text-white">Blog Coming Soon</h2>
                <p className="mt-2 text-lg text-slate-400">I'm currently writing articles on data analysis, machine learning, and career development.</p>
            </div>
        </div>
    );
};

const ContactPage = () => {
    const fadeInProps = useFadeIn();
    return (
        <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-16" {...fadeInProps}>
            <div className="text-center py-24 bg-slate-800/50 rounded-lg">
                <MessageSquare size={48} className="mx-auto text-blue-400" />
                <h2 className="mt-6 text-3xl font-bold text-white">Get In Touch</h2>
                <p className="mt-4 text-lg text-slate-400">Feel free to reach out for collaborations or just a friendly chat.</p>
                <div className="mt-8 flex justify-center items-center space-x-6">
                    <a href="mailto:fretchtroy.ybanez@gmail.com" className="text-slate-400 hover:text-blue-400 transition-colors">
                        <Mail size={28} />
                    </a>
                    <a href="https://www.linkedin.com/in/fretch-royette-yba%C3%B1ez-58a975247/" target="_blank" rel="noopener noreferrer" className="text-slate-400 hover:text-blue-400 transition-colors">
                        <Linkedin size={28} />
                    </a>
                    <a href="https://github.com/Fretch-troy1001" target="_blank" rel="noopener noreferrer" className="text-slate-400 hover:text-blue-400 transition-colors">
                        <Github size={28} />
                    </a>
                </div>
            </div>
        </div>
    );
};

// --- Footer ---
const Footer = ({ navigateTo }) => {
    return (
        <footer className="bg-slate-800/50 border-t border-slate-700 mt-24">
            <div className="max-w-7xl mx-auto py-6 px-4 sm:px-6 lg:px-8 text-center text-sm text-slate-400">
                <p>&copy; {new Date().getFullYear()} Fretch Royette Ybañez. All Rights Reserved.</p>
                <p className="mt-2">Built with React & Tailwind CSS.</p>
            </div>
        </footer>
    );
};

export default App;
