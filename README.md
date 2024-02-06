# ICLR20204-FMP: Adversarial Feature Map Pruning for Backdoor

<a href="https://arxiv.org/abs/2307.11565"><img src="https://img.shields.io/badge/arXiv-Paper-<color>"></a>

## Paper Abstract
Deep neural networks have been widely used in many critical applications, such as autonomous vehicles and medical diagnosis. However, their security is threatened by backdoor attack, which is achieved by adding artificial patterns to specific training data. Existing defense strategies primarily focus on using reverse engineering to reproduce the backdoor trigger generated by attackers and subsequently repair the DNN model by adding the trigger into inputs and fine-tuning the model with ground-truth labels. However, once the trigger generated by the attackers is complex and invisible, the defender can not successfully reproduce the trigger. Consequently, the DNN model will not be repaired since the trigger is not effectively removed.
In this work, we propose Feature Map Testing~(FMT). Different from existing defense strategies, which focus on reproducing backdoor triggers, FMT tries to detect the backdoor feature maps, which are trained to extract backdoor information from the inputs. After detecting these backdoor feature maps, FMT will erase them and then fine-tune the model with a secure subset of training data. Our experiments demonstrate that, compared to existing defense strategies, FMT can effectively reduce the Attack Success Rate (ASR) even against the most complex and invisible attack triggers. Second, unlike conventional defense methods that tend to exhibit low Robust Accuracy (i.e., the model's accuracy on the poisoned data), FMT achieves higher RA, indicating its superiority in maintaining model performance while mitigating the effects of backdoor attacks~(e.g., FMT obtains 87.40\% RA in CIFAR10). Third, compared to existing feature map pruning techniques, FMT can cover more backdoor feature maps~(e.g., FMT removes 83.33\% of backdoor feature maps from the model in the CIFAR10 \& BadNet scenario).

## How to run FMT for different attack?

### First, generate injected model

Taking badnet and cifar10 dataset as a example.
```
python ./attack/badnet_attack.py --yaml_path ../config/attack/badnet/cifar10.yaml --dataset cifar10 --dataset_path ../data --save_folder_name badnet_cifar10
```

### Second, use FMT to repair DNN model.

```
python ./defense/feature.py  --yaml_path ./config/defense/feature/cifar10.yaml --dataset cifar10 --result_file badnet_cifar10
```

### Then, run baseline approaches~(e.g., FT).

```
python ./defense/ft/ft.py --result_file badnet_cifar10 --yaml_path ./config/defense/ft/cifar10.yaml --dataset cifar10
```
