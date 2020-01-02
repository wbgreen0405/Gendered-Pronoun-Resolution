## Gendered-Pronoun-Resolution

🥈 | `Silver Medal` | 26th place out of 838 competitiors. 

Team Members: 

 [Wayward Artisan](https://www.kaggle.com/taniaj)

 [Arigion](https://www.kaggle.com/arigion)
              
 [Ivan Panshin](https://www.kaggle.com/ivanpan)
              

Pair pronouns to their correct entities

1. We didn't manage to fine-tune Bert, but still had a couple of ideas that worked pretty good.

2. Used Bert-large with concatenated embeddings from -3, -4, -5, -6 layers. As [Ceshine Lee](https://www.kaggle.com/ceshine) pointed out in his great [kernel](https://www.kaggle.com/ceshine/pytorch-bert-endpointspanextractor-kfold), it's better not to use the last layer. After some experimentation, we settled on -3, -4, -5, and -6 layers based on CV scores.

3. We used [corrected and original data](https://www.kaggle.com/c/gendered-pronoun-resolution/discussion/81331#latest-503495). We couldn't decide which models to choose: the ones that were trained on original or corrected data. Until we tried to blend them and it worked great (0.34-0.35 for original/corrected and 0.33 after the blending for Public LB). Our 2 final submissions were only different in terms of weights in blending. We tried 0.6/0.4 and 0.5/0.5 for corrected/original data. Just like in Public LB, 0.6/0.4 split worked better (0.24838 vs 0.25200 Private LB)

4. Applied data augmentation inside each fold by simply swapping A and B columns and concatenating with original data.

5. 10 folds, of course.

6. A simple NN (4 layers with BN, ReLU and dropout) on top of bert embeddings and linguistic features from public kernels. More complicated architectures didn't bring anything to the table.
