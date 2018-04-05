# Knowledge-from-Local-Soft-Targets

## Rethinking about the CrossEntropy Loss
Onehot is a vector that represents the classification ground truth in a sparse vector, where only the correct index is 1 and all others are 0. Onehot is widely used in learning tasks such as classification. However, by using onehot as the ground truth, the hidden relation between classes are omitted. 

For example, we now want to classify whether this object belongs to dog, cat or wall. 

  P  | dog | cat | wall
 ---|---|---|---
 gt | 1 | 0 | 0
 pred@1 | 0 | 1 | 0
 pred@2 | 0 | 0 | 0
 
When the correct answer is gt:[1, 0, 0] (dog), two predictions [0, 1, 0] (cat) and [0, 0, 1] (wall) are penalized equally. But we know class “cat” is more similar to class “dog” than class "wall". Though the two predictions are both wrong, prediction “cat” appears nire reasonable than prediction “wall”, hence should not be penalized equally.  
 
Soft targets provide stronger information, but how to collect soft targets for dataset becomes the next problem. Manually marking is usually too costy to afford. Some works use the voting result of several heavy teacher models, though much cheaper, the workload of pretraining is still unacceptable when dataset is large. 

