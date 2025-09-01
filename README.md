#DATING RED FLAG ANALYSIS - Analyzing  dating bios with NLP & fun visualizations

#INTRODUCTION

- This project is a Red Flag Analysis. It analyzes Dating bios and classifies them into commonly used Gen Z dating flags: Green Flag (sweet, genuine), Red Flag (toxic, chaotic), Mixed Flag.
- In this project, I'm focusing on analyzing the red flags in dating bios and turning them into fun visualizations.

#PURPOSE

Bios on dating apps on social media work as a shortcut to knowing a person - they often reveal a lot in just few lines. But not all bios are positive: many carry red flags that hint at toxic or chaotic behavior.
The purpose of this project is to analyze those bios and understand what percentage of them fall under red flags, compared to green or mixed ones. I also wanted to make the process more fun by adding unique, Gen -style
visualizationsinstead of plain boring graphs. 

#DATA

The dataset consists of more than 3000 bios (approximately 3,095). These bios are AI-generated to mimic human-like dating bios. I avoided including real bios from actual people, since that would breach privacy. 
Instead, the AI-generated dataset provides realistic examples.

Additional fields such as city, gender, age and platform are also sysnthetic (no real).

-Cities: Houston, Chicago, Las Vegas, San Fransisco, New York, LA, Dallas, Philadelphia
-Gneder: Male, Female, Non-binary
-Age Range: 18 to 45 
-Platform: Tinder, Hinge, Bumble, OkCupid, Coffee Meets Bagel (CMB)
These attributes were randomly assigned using python's random.choices function. 
The final dataset is stored in the file: real_authentic_dating_bios.csv

#DATA PREPROCESS
   
-Lowercasing, Punctuation Removal: Since the dataset and rows were messy and raw, I applied various text cleaning steps. Some bios were written in caps, some in small letters, and some mixed. So, for analysis, I converted all bios into lowercase.
I also removed special characters and punctuation, which were just unnecessary clutter.

-Numbers and Emoji Removal: Next, I removed numbers and emojis. Emojis don’t really add much analytical value, and sometimes they even give false signals (for example, the recent trend of using a rose emoji 🥀 as a broken heart symbol 
instead of the actual broken heart 💔 emoji). To avoid such confusion, I dropped them.

-Tokenization and Handling Contractions: I then applied tokenization, which breaks bios into smaller segments (tokens). After that, I handled contractions, so words like don’t and do not are treated as the same.

-Stopwords Removal and Lemmatization with POS tagging: The second-to-last step was filtering tokens, which removes stopwords like in, a, the. Finally, I applied lemmatization, which reduces words to their base form. 
for example, dancing and dance are understood as the same. I also used lemmatization with POS tagging so that the algorithm could recognize whether a word is a noun or a verb, making the analysis more accurate.

The Final cleaned dataset saved as bios_cleaned_preview.csv with columns like bio_cleaned, tokens, filtered_tokens, lemmatized_tokens.

#WORD ANALYSIS

-Word Frequency (Counter):
I used this to find the most common words from the bios. For example, the word “I” was used 543 times, and “and” was used 388 times. This helps in knowing which words appear the most overall.

-Bigram Analysis
I used this to check which words are most often used together. For example, the result showed “obsessed with”. By seeing this, we can guess it might lean toward a red flag, 
but it’s not always the case—people can also use it in a casual or positive way, like “obsessed with coffee.” It’s a minor thing, but overall the word “obsessed” tends to lean towards red.
From this, we can understand word pairings better and use them later in flag classification.

-Stopword Removal
In this step, I removed stopwords and then checked which words appeared the most. In the earlier word frequency analysis, words like “I” and “and” showed up a lot, 
but they don’t really add any value in flag classification. So after removing stopwords, I got more meaningful words like “loves,” “coffee,” and “chaos,” which help much more in further classification.

TF-IDF
From this, we get a score of how important a word is compared to others across the dataset. It basically highlights words that stand out more than just being frequently repeated.
 
#FLAG CLASSIFICATION

For flag classification, I created three keyword sections:

green_flag = [ .... ]
red_flag = [ .... ]
mixed_flag = [ .... ]

These keywords were detected in two ways:

1. Manual checking of a sample of bios.
2. Word analysis results (like frequency, bigrams, etc.).
Then I applied a rule-based classification where the system matches bios with these keywords:
If a keyword from the red_flag section is found then output: 🚩 Red Flag
If a keyword from the green_flag section is found then output: 🌿 Green Flag
If a keyword from the mixed_flag section is found then output: 🙂 Mixed Flag
If no keyword matches then output: 🤷‍♀️ No clear signal

The results were then saved into a CSV file named flags_classification.csv, which includes the following columns:
-bio
-gender
-age
-city
-platform
-filtered_tokens
-lemmatized_tokens
-flag_classification
-reason (shows the exact word that triggered the classification)


#VISUALIZATION AND INSIGHTS:

1) Pie Chart - Dating Cake:
   The first visualization is a pie chart that breaks down the flag classifications by color:

🚩 Red Flag → Red
🌿 Green Flag → Green
🙂 Mixed Flag → Yellow
🤷‍♀️ No Clear Signal → Gray

The shocking part? Out of ~3,095 bios, around 1,083 (35.1%) fall under the red flag category. That’s more than a third of the dataset!
Why so high? A big reason is that many bios casually drop words like “casual,” “toxic,” “bad,” “obsessed”—and because this is a rule-based word classification, every keyword carries weight. 
For example, just adding the word “casual” is enough to push a bio straight into the 🚩 zone.


2) Horizontal Bar Chart - The Toxicity Race 🏆🚩:

This visualization is designed as a race between age ranges to see which group is leading in toxicity. To make it more engaging, I added characters running on the bars,
 almost like they’re competing for the gold trophy.

The bars are shaded from light red to dark red:
🔴 Light red → slower runners (less toxic)
🩸 Dark red → fastest runners (most toxic, leading the race)

And here’s the fun twist:
The 25–34 age group (393 red flags) and the 35–44 age group (384 red flags) were in a neck-to-neck race, almost sprinting side by side for the gold trophy 🥇.
The slowest runner? Age 45+, far behind in the race with the least number of red flags 🐢.
This makes it super easy to see which age group is dominating the “toxicity race” and which ones are lagging behind.


3) Hotspot Map: City Toxicity Heatmap 🗺️🚨

   [Click here to view the interactive map](https://rawcdn.githack.com/KshitijaNikale/Dating-Bios-Red-Flag-Analysis/refs/heads/main/toxic_city_map.html)

This visualization zooms into 8 major cities and highlights them in light-to-dark shades, depending on how many red-flag bios each city contains. 
The darker the shade, the more toxic energy the city is radiating 🌡️.

The map does double duty:
On hovering over a city, you don’t just see the red flag count—you also see which platforms those bios came from.
Each platform is color-coded, making it easy to spot whether toxicity is brewing more on, say, Tinder 🔥, Bumble 🐝, or Hinge 💘.
Tinder is indicated by blue color, CMB by black color, okCupid by purple , Hinge by green.

So in one glance, you can answer two questions:
1. Which city is a red flag capital? 🏙️
2. Which dating platforms are driving the toxicity in that city? 📱

This way, the map becomes not just a geographic hotspot chart, but also a platform battle of red flags.

Together these visualzation turns raw bios into a story : showing how age, city, and even platforms compete in the ultimate red flag Olympics. 🏆🚩

#RESULTS & KEY TAKEAWAYS: 

• Pie chart showed that in bios the classification of red flags is more than any other classification (35.1%). This shows that a large chunk of bios were red flag (1000+). 
  And This is all because people keep using words like obsessed, casual, toxic etc in their bios a lot. which adds them in the category of red flags.

• The count of Green flags in the pie chart was less then red flags by just 2% (33.0%). This shows that there are still green flags out there. 
  The classification of green flag is also more because people use words like Love, life etc.
  This type words are defined in the green_flag keyword list. So even if the bios are something like 'love to lie' it will still be classified as green flag because of the word love in it. 
  Thats why, I have also added dual words or two words in the keyword list. 

• Mixed Flags give confusing vibes becuase they include both (green & red) kind of words in their bios. 

• The most interesting and fun part of the project is the race between age groups. the age range 25-34 and 35-44 were in almost neck to neck competition where anyone from them can win 
  (384 red flag counts vs 383 red flaf counts). The slowest players in the race were the 45+. 

• The Hotspot showed which part of the cities were most toxic and which platform is mostly been active by the red flags.

*Overall takeaway - Dating bios are not as innocent as they look. One tiny keyowrd is enough to paint a whole bio red. 

#LIBRARIES & TOOLS: 

• Pandas
• NLTK
• Matplotlib & PLotly
• Jupyter Notebook

#ACKNOWLEGEMENT / INSPIRATION:

• Inspired by everyday observations on how much people say about themselves in just a short bio.
• Took cues from Gen Z Internet humor, and behavioral science ideas like shortcuts in human judgement.
• Visualization styles inspired by a mix of data storytelling.


#CONTACT INFO:

•💌 wanna connect? : Linkdin- https://www.linkedin.com/in/kshitija-nikale-9935122b1/
                     Email - kshitijanikale4@gmail.com


