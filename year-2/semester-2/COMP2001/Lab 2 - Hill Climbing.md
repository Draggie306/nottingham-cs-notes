Comparing Davis’s Bit Hill Climbing to Steepest Descent, with a budget of 1 second on the CPU, Davis’s bit finds a (locally optimal) solution much more quickly, whereas SDHC is still making improvements.

Different instances may have more or less rugged search landscapes. The more rugged the search landscape, the faster we get stuck in a local optimum.

In some cases, changing the hill climbing algorithm to accept moves of better OR equal values results in a better solution because it may choose a different neighbouring solution when there are multiple solutions of the same quality.