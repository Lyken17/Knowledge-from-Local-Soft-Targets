# Knowledge-from-Local-Soft-Targets

## Rethinking about the CrossEntropy Loss
Onehot is a vector that represents the classification ground truth in a sparse vector, where only v[correct] is 1 and all others are 0. Onehot is widely used in various tasks. However, by using onehot as the ground truth, the hidden relation between classes are omitted. 

For example, we now want to classify whether this object belongs to dog, cat or wall. 

  P  | dog | cat | wall
 ---|---|---|---
 gt | 1 | 0 | 0
 pred@1 | 0 | 1 | 0
 pred@2 | 0 | 0 | 0
 
 When the correct answer is gt:[1, 0, 0] (dog), two predictions [0, 1, 0] (cat) and [0, 0, 1] (wall) are penalized equally. But obviously class “cat” is more similar to class “dog”. In this case, though two predictions are both wrong, the prediction “cat” is more reasonable than prediction “wall”, hence should not be penalized equally.  
 
Soft targets provide stronger information, but how to collect soft targets for dataset becomes the next problem. Manually marking is usually too costly to afford. Previous works [7, 8] use the voting result of several heavy teacher models, though much cheaper, the workload of pretraining is still unacceptable when dataset is large. 

