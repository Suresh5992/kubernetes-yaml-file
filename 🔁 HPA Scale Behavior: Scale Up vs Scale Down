🔁 HPA Scale Behavior: Scale Up vs Scale Down


| Feature                       | Scale Up                                | Scale Down                                  |
|------------------------------|-----------------------------------------|---------------------------------------------|
| **Wait Time**                | 30 seconds                              | 60 seconds                                  |
| **Policy 1**                 | Add up to **2 pods** every 30 seconds   | Remove up to **50%** of pods every 60 sec   |
| **Policy 2**                 | *(Only one policy defined)*             | Remove up to **1 pod** every 60 seconds     |
| **selectPolicy**             | `Max` → add more pods                   | `Max` → remove more pods (50% or 1 pod)     |


✅ Example Scenario (Markdown)



| Time   | Event             | Scale Up Action                          | Scale Down Action                         |
|--------|-------------------|------------------------------------------|-------------------------------------------|
| 00:00  | High CPU detected | Add 2 pods → total 6                     | —                                         |
| 00:30  | High CPU continues| Add 2 more pods → total 8                | —                                         |
| 01:00  | CPU drops         | —                                        | Remove 2 pods (50% of 4) → total 2        |
| 02:00  | Still low usage   | —                                        | Remove 1 pod → total 1                    |
