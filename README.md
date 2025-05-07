# SeqRecPapers

Awesome Papers in Sequential Recommendation

## Conventional Baselines

### SASRec (ICDM '18)

This paper ...

- **Title**: [Self-Attentive Sequential Recommendation](https://ieeexplore.ieee.org/abstract/document/8594844)
- **Code**: ...
- **Citation**: Kang, Wang-Cheng, and Julian McAuley. "Self-attentive sequential recommendation." 2018 IEEE international conference on data mining (ICDM). IEEE, 2018.

## Contrastive Learning for SeqRec

### CL4SRec

The paper proposes a novel model called **Contrastive Learning for Sequential Recommendation (CL4SRec)**. It also proposes three data augmentation approaches: mask, crop and reorder.

The contrastive learning framework is as follows: Two data augmentation methods, $a_i$ and $a_j$ , are sampled from the same augmentation set A. They are applied to each user’s sequence and then we can obtain two correlated views of each sequence. A shared embedding layer and the user representation model f (·) (transformer in this paper) transform the original and augmented sequences to the latent space where the contrastive loss and recommendation loss are applied. The final loss function is the linear weighted sum of conrastive loss and recommendation loss.

- **Title**: [Contrastive Learning for Sequential Recommendation](https://ieeexplore.ieee.org/document/9835621)
- **Code**: https://github.com/JamZheng/CL4SRec-pytorch
- Citation: X. Xie et al., "Contrastive Learning for Sequential Recommendation," 2022 IEEE 38th International Conference on Data Engineering (ICDE), Kuala Lumpur, Malaysia, 2022, pp. 1259-1273, doi: 10.1109/ICDE53745.2022.00099.

### LACLRec

This paper introduces a novel framework called **Learnable Sequence Augmenter for Triplet Contrastive Learning in Sequential Recommendation (LACLRec)**. 

Specifically, a **self-supervised learning-based augmenter** is designed to automatically delete noisy items and insert new items that better capture item transition patterns, thereby generating higher-quality augmented sequences. The augmenter is trained using a self-supervised learning task where it learns to restore sequences that have been randomly modified. The augmenter can perform three operations: `keep`, `delete`, and `insert`. For the `insert` operation, a reverse generator calculates the probability of each candidate item being inserted, allowing the insertion of a subsequence rather than just a single item. 

Subsequently, LACLRec employs a **triplet contrastive learning approach**, where the raw sequence, an SSL-augmented sequence, and a randomly augmented sequence are used to provide more fine-grained contrastive signals. Two types of contrastive losses are used:  
1. Coarse-Grained Contrastive Loss($L_{cl}$): This loss maximizes the similarity between two augmented sequences derived from the same raw sequence while minimizing their similarity with other negative samples.
2. Fine-Grained Triplet Contrastive Loss ($L{tri}$): This loss directly maximizes the similarity between the raw sequence and the SSL-augmented sequence while minimizing the similarity between the raw sequence and the randomly augmented sequence.
The paper concludes that LACLRec effectively mitigates issues of data sparsity and noisy interactions in sequential recommendation by employing a learnable augmenter and a triplet contrastive learning framework.

- **Title**: [Learnable Sequence Augmenter for Triplet Contrastive Learning in Sequential Recommendation](https://arxiv.org/abs/2503.20232)
- **Code**: Not provided
- **Citation**: Wang, Wei, et al. "Learnable Sequence Augmenter for Triplet Contrastive Learning in Sequential Recommendation." arXiv preprint arXiv:2503.20232 (2025).



## Scaling

### Scalable Recommendation Transformer

This work studied **the scaling behavior of the transformer architecture**. 

To make a scalable transformer-based model, the paper introduced a simple and flexible architecture called **Scalable Recommendation Transformer (SRT)**. Traditional transformer-based recommendation models learn vector embeddings for all items in the catalog and access them via LUT (maybe adding a classification layer). SRT use **a fixed (and task-agnostic) feature extractor** to encode the items and to predict item-to-item similarities using the output embeddings of the transformer model. We use the last element of the sequence as target and try to match its id (classification) or input embedding (regression).

For learning formulation that can scale the SeqRec problem, it proposed a scaling strategy. The strategy consists of sampling users at random and recording their interactions into a single dataset. Note that by increasing the number of active users, we account for a more extensive set of items they interact with.

It showed there exist scaling laws in SeqRec similar to those observed in other sequential prediction domains. 

The work also shows that by **pre-training larger recommendation transformers**, we can **fine-tune them for downstream tasks** with significantly lesser data and obtain performance improvements compared to the same models trained from scratch.

- **Title**: [Scaling Sequential Recommendation Models with Transformers](https://arxiv.org/abs/2412.07585)
- **Code**: https://github.com/mercadolibre/srt
- Citation: P. Zivic, H. Vazquez, and J. Sánchez, "Scaling Sequential Recommendation Models with Transformers," in Proceedings of the 47th International ACM SIGIR Conference on Research and Development in Information Retrieval (SIGIR '24), Washington, DC, USA, 2024, pp. 1567–1577, doi: 10.1145/3626772.3657816.



### Insights into Large Recommendation Models

Several insghts are introduced in this paper through experiments

1. Model size is proportional to O(LD).

2. Larger datasets should be matched with larger models

3. Performance does not consistently improve with increasing model size. Upon reaching a peak, performance begins to fluctuate, highlighting the need for guidelines to align model size with dataset size for optimal performance.

4. **Residual connection pattern** and the **relative attention bias** contribute to enhancing the scalability of traditional recommendation models.
5. A **well-normalized model** may enhance both scalability and recall performance.
6. The paper observed scaling law in behavior modeling with side information,  multi-behavior modeling and multi-domain modeling.

Additionally, the paper explored the performance and scaling laws of HSTU in ranking tasks.

- **Title**:  [Scaling New Frontiers: Insights into Large Recommendation Models](https://arxiv.org/abs/2412.00714)
- **Code**: https://github.com/USTC-StarTeam/Awesome-Large-Recommendation-Models
- **Citation**: Guo, W., “Scaling New Frontiers: Insights into Large Recommendation Models”, <i>arXiv e-prints</i>, Art. no. arXiv:2412.00714, 2024. doi:10.48550/arXiv.2412.00714.



### ApEn

**Structural and collaborative issues** in recommender systems prevents the direct application of the Scaling Law (SL) . 

The paper propose **Approximate Entropy (ApEn)**, a statistical measure used to quantify the regularity and unpredictability of time series data.

For a given time series $\{x_i\}$ of length $N$ and parameters $m$ (emb_dim) and $r$ (tolerance),  construct  $X_i = [x_i, x_{i+1}, . . . , x_{i+m−1}] \text{ for } i = 1, . . . , N − m + 1$. 

the **distance** between $X_i$ and $X_j$ is  $d[X_i, X_j] = max_{0≤k<m} |x_{i+k} − x_{j+k}|$.

the **similarity measure** is $C^m_i (r) = \frac{|\{j | d[X_i, X_j] ≤ r\}|}{N-m+1}$and the average similarity $Φ^m(r) = \frac{1}{N −m+1} \sum^{N-m+1}_  {i=1}  ln C^m_i (r)$. 

The **Approximate Entropy** : $ApEn(m, r, N ) = Φ^m(r) − Φ^{m+1}(r)$.

**In fact,** $ ApEn = −E_j(log P(|x_{j+m} − x_{m+1}| ≤ r ∥  |x_{j+k−1} − x_k| ≤ r\text{ for } k = 1, 2, .., m)$ 

ApEn has **a postive correlation with the model’s duplication rate**.

the paper introduces **the Performance Law for SR models**, 

$$
\text{Performance} = w_1(\log N + \frac{p_1}{N^{w_3}} )+  w_2(\log d_{emb} + \frac{p_1}{d^{w_4}_{emb}}  ) + \log D' + \frac{p_2}{D'^{w5}}
$$
Where $ D' = \# Tokens \times ApEn'$ represents the data parameter, $N$ is the number of model layers, and $d_{emb}$ is the item embedding dimension, performance here could be HR@10, NDCG@10.

This can be utilized in **golobal and local optimal parameter search** or **exploring scaling Law potential among framwork**.


- **Title**: [Optimizing Sequential Recommendation Models with Scaling Laws and  Approximate Entropy](https://arxiv.org/abs/2412.00430)
- **Code**: Not provided
- **Citation**: Shen, T., “Optimizing Sequential Recommendation Models with Scaling Laws and Approximate Entropy”, <i>arXiv e-prints</i>, Art. no. arXiv:2412.00430, 2024. doi:10.48550/arXiv.2412.00430.
