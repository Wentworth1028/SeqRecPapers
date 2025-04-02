# SeqRecPapers

Awesome Papers in Sequential Recommendation

## Conventional Baselines

### SASRec (ICDM '18)

This paper ...

- **Title**: [Self-Attentive Sequential Recommendation](https://ieeexplore.ieee.org/abstract/document/8594844)
- **Code**: ...
- **Citation**: Kang, Wang-Cheng, and Julian McAuley. "Self-attentive sequential recommendation." 2018 IEEE international conference on data mining (ICDM). IEEE, 2018.

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
