## Gendered Pronoun Resolution 🥈 | `Silver Medal` | 26th out of 838 

Can you help end gender bias in pronoun resolution?
==============================

Pronoun resolution is part of coreference resolution, the task of pairing an expression to its referring entity. This is an important task for natural language understanding, and the resolution of ambiguous pronouns is a longstanding challenge.

Unfortunately, recent studies have suggested gender bias among state-of-the-art coreference resolvers. Google AI Language aims to improve gender-fairness in modeling by releasing the Gendered Ambiguous Pronouns (GAP) dataset, containing gender-balanced pronouns (50% of its examples containing feminine pronouns, and 50% containing masculine pronouns).

Team Members: 

 [Wayward Artisan](https://www.kaggle.com/taniaj)

 [Arigion](https://www.kaggle.com/arigion)
              
 [Ivan Panshin](https://www.kaggle.com/ivanpan)
              

We did not did not fine-tune Bert, but still had a couple of ideas that worked pretty well. We used a Bert-large with concatenated embeddings from -3, -4, -5, -6 layers. As [Ceshine Lee](https://www.kaggle.com/ceshine) pointed out in his great [kernel](https://www.kaggle.com/ceshine/pytorch-bert-endpointspanextractor-kfold), it's beneficial not to use the last layer. After some experimentation, we settled on -3, -4, -5, and -6 layers based on CV scores.

We used [corrected and original data](https://www.kaggle.com/c/gendered-pronoun-resolution/discussion/81331#latest-503495). We couldn't decide which models to choose: the ones that were trained on original or corrected data. Until we tried to blend them and it worked great (0.34-0.35 for original/corrected and 0.33 after the blending for Public LB). Our 2 final submissions were only different in terms of weights in blending. We tried 0.6/0.4 and 0.5/0.5 for corrected/original data. Just like in Public LB, 0.6/0.4 split worked better (0.24838 vs 0.25200 Private LB).

We applied data augmentation inside each fold by simply swapping A and B columns and concatenating with original data.
We train a simple NN (4 layers with BN, ReLU and dropout) on top of bert embeddings and linguistic featureour model for 10 folds. Sophisicated models did not work in our favor and we determine to use those models. 
