---
title:  "Evaluation for survival modeling(C-statistic)"
date:   2021-08-02

categories: R Python

toc: false
toc_label: "overview"
excerpt: "python code for Concordance-index (C-statistic)"
---
Evaluation of the ability of a survival model to predict future data is the most important consideration in the development of prediction model. The primary metric used to evaluate survival models is the concordance index, also known as C-statistic. The idea of the concordance index is that a good model should rank individuals who survive longer higher than individuals who die sooner. 

To formulate this mathematically, consider the function produced by the survival model, <i>S(E)</i>, that gives a score to event E indicating the relative time at which E occurs. E<sub>i</sub> is uncensored event observed in the dataset, whereas E<sub>j</sub> is any events, censored or not censored.

![math_func1](/pics/ARDS/math_func1.png)

In plain words :

![math_func3](/pics/ARDS/permissible.png)

Here is the handcraft python code to compute Harrel's C-index. 
 

```yml
def harrell_c(y_true, scores, event):
    '''
    Compute Harrel C-index given true event/censoring times,
    model output, and event indicators.
    
    Args:
        y_true (array): array of true event times
        scores (array): model risk scores
        event (array): indicator, 1 if event occurred at that index, 0 for censorship
    Returns:
        result (float): C-index metric
    '''
    
    n = len(y_true)
    assert (len(scores) == n and len(event) == n)
    
    concordant = 0.0
    permissible = 0.0
    ties = 0.0
    
    result = 0.0
           
    # use double for loop to go through cases
    for i in range(n):
        # set lower bound on j to avoid double counting
        for j in range(i+1, n):
            
            # check if at most one is censored
            if not (event[i] == 0 and event[j] == 0):
                #pass
            
                # check if neither are censored
                if event[i] == 1 and event[j] == 1:
                    permissible += 1
                    
                    # check if scores are tied
                    if y_true[i] == y_true[j]:
                        ties += 1
                    
                    # check for concordant
                    elif y_true[i] > y_true[j] and scores[i] < scores[j]:
                        concordant += 1
                    elif y_true[i] < y_true[j] and scores[i] > scores[j]:
                        concordant += 1
                # check if one is censored
                elif event[i] == 0 or event[j] == 0:
                    
                    # get censored index
                    censored = j
                    uncensored = i
                    
                    if event[i] == 0:
                        censored = i
                        uncensored = j
                        
                    # check if permissible

                    if y_true[censored] >= y_true[uncensored]:
                        permissible += 1
                        
                        # check if scores are tied
                        if scores[i] == scores[j]:
                            # update ties 
                            ties += 1
                            
                        # check if scores are concordant 
                        if y_true[censored] >= y_true[uncensored] and scores[censored] < scores[uncensored]:
                            concordant += 1
    
    # set result to c-index computed from number of concordant pairs,
    result = (concordant + 0.5 * ties) / permissible
       
    return result
```





---