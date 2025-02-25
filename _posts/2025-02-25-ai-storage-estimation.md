---
title: "How AI is 10x'ing my Team Performance"
tags:
  - ChatGPT
  - Gen-AI
  - LLM
  - DataTeam
toc: true
---

<figure>
	<a href=""><img src="https://i.imgur.com/VZ002aL.jpeg"></a>
</figure>

Artificial Intelligence (AI) has become a transformative force in the field of data science, enabling teams to achieve unprecedented levels of efficiency and scalability. I this article I wanted to showcase how embracing AI can lead to **10x the performance of your data team**, leveraging its capabilities to automate routine tasks, enhance decision-making, and optimise resource allocation. In this article, I’ll share a practical example of how AI was used to solve a critical problem: determining storage requirements for Redis in a scalable system.


### Tackling the Ticket: Redis Storage Estimation

One of the recent challenges required determining the storage requirements for provisioning Redis. The goal was to estimate how much memory Redis would need to store player data for a new model, based on varying payload sizes and player counts.

The Redis key-value structure we used was as follows:

- **Key**: `ds-gre-last-played:{tenant_id}:{player_id}`
- **Value**:

```json
{
  "casino": {"game_ids": [game_1, game_2, ..., game_n], "last_played": dt, "last_update_dt": dt},
  "sports": {"event_ids": [game_1, game_2, ..., game_n], "last_played": dt, "last_update_dt": dt},
  "sweep": {"game_ids": [game_1, game_2, ..., game_n], "last_played": dt, "last_update_dt": dt}
}
```


The task involved calculating the required storage for payloads containing 20 games per vertical (casino, sports, sweep) and scaling up to 100 games in increments of 10. This calculation had to account for **1 million players**.



### Using AI to Automate Analysis

Traditionally, this ticket would have taken a mid-level data scientist between **1–2 hours** to complete. However, by leveraging AI tools and techniques, specifically **ChatGPT**, I was able to complete the task in just **5 minutes**. This dramatic reduction in time highlights the power of AI in automating repetitive yet essential tasks.

To solve the problem efficiently, I used ChatGPT to generate a Python script that automated the entire analysis process. The prompt I used for this task is:
```txt
I need to answer the question - How large will I need to provision Redis? To do this, assuming a payload of 20 games per vertical (verticals are casino, sports and sweep), get the size required in to have a key-value in Redis as per the key-value sample below, multiply by this size by 1,000,000 players. Repeat for 30, 40, 50, all the way up to 100, in increments of 10 games. The redis key should be of type:

KEY: ds-gre-last-played:{tenant_id}:{player_id}

VALUE:

{
  casino: {game_ids  : [game_1, game_2, ...., game_n], last_played: dt, last_update_dt: dt}, 
  sports :{event_ids  : [game_1, game_2, ...., game_n], last_played: dt, last_update_dt: dt}, 
  sweep : {game_ids  : [game_1, game_2, ...., game_n], last_played: dt, last_update_dt: dt}
  }

Write a Python script that does this analysis for me
```


Below is the code provided by the AI:

```python
import json
import sys

def estimate_redis_size(num_games_per_vertical):
    sample_key = "ds-gre-last-played:{tenant_id}:{player_id}"
    tenant_id = "12345"
    player_id = "67890"
    
    # Example timestamps (these will be stored as strings in JSON)
    last_played = "2025-02-24T12:00:00Z"
    last_update_dt = "2025-02-24T12:30:00Z"
    
    # Constructing the sample value
    sample_value = {
        "casino": {"game_ids": [f"game_{i}" for i in range(num_games_per_vertical)], "last_played": last_played, "last_update_dt": last_update_dt},
        "sports": {"event_ids": [f"event_{i}" for i in range(num_games_per_vertical)], "last_played": last_played, "last_update_dt": last_update_dt},
        "sweep": {"game_ids": [f"game_{i}" for i in range(num_games_per_vertical)], "last_played": last_played, "last_update_dt": last_update_dt}
    }
    
    # Convert to JSON and estimate size in bytes
    key_size = len(sample_key.replace("{tenant_id}", tenant_id).replace("{player_id}", player_id))
    value_size = len(json.dumps(sample_value))
    entry_size = key_size + value_size
    
    # Multiply by 1,000,000 players
    total_size = entry_size * 1_000_000
    total_size_mb = total_size / (1024 * 1024)  # Convert to MB
    total_size_gb = total_size_mb / 1024  # Convert to GB
    
    return num_games_per_vertical, entry_size, total_size_mb, total_size_gb

if __name__ == "__main__":
    print("Games per Vertical | Entry Size (bytes) | Total Size (MB) | Total Size (GB)")
    print("-" * 65)
    for num_games in range(20, 101, 10):
        games, entry_size, total_size_mb, total_size_gb = estimate_redis_size(num_games)
        print(f"{games:<18} | {entry_size:<18} | {total_size_mb:<12.2f} MB | {total_size_gb:.2f} GB")
```


### Results and Insights

This is the ChatGPT interface which allows you to run code on your browser. 

<figure>
	<a href=""><img src="https://i.imgur.com/rtsKE8t.png"></a>
</figure>

The script provided insights into how storage requirements scaled with the number of games per vertical. The output showed:

```
Games per Vertical | Entry Size (bytes) | Total Size (MB) | Total Size (GB)
---------------------------------------------------------------------------
20                 | 1001               | 954.63 MB       | 0.93 GB
30                 | 1341               | 1278.88 MB      | 1.25 GB
40                 | 1681               | 1603.13 MB      | 1.57 GB
50                 | 2021               | 1927.38 MB      | 1.88 GB
60                 | 2361               | 2251.63 MB      | 2.20 GB
70                 | 2701               | 2575.87 MB      | 2.52 GB
80                 | 3041               | 2900.12 MB      | 2.83 GB
90                 | 3381               | 3224.37 MB      | 3.15 GB
100                | 3721               | 3548.62 MB      | 3.47 GB
```

These results allowed us to provision Redis with confidence, ensuring sufficient memory while avoiding over-allocation. By automating this analysis with AI-generated code, what would have taken hours of manual effort was completed in mere minutes.



### The Impact of AI on Productivity

This example demonstrates how AI is fundamentally changing how we approach problem-solving in data science. By integrating AI into our workflows:

1. **Efficiency Gains**: Tasks that previously required manual intervention are now automated.
2. **Time Savings**: A task that would have taken a mid-level scientist up to two hours was completed in just five minutes.
3. **Scalability**: We can handle larger datasets and more complex use cases without additional strain on resources.
4. **Accuracy**: AI minimises human error in calculations and coding.



### Final Thoughts

AI has proven instrumental in enhancing our data science team’s performance. From automating routine tasks like storage estimation to enabling more strategic decision-making through data-driven insights, it has become an integral part of our operations.

[^1]: https://www.linkedin.com/pulse/10x-data-scientists-bojan-tunguz-ph-d-

[^2]: https://nogood.io/2025/01/31/10x-ai-marketer/

[^3]: https://www.keboola.com/blog/how-to-be-10x-more-productive-than-the-average-data-scientist

[^4]: https://blog.outsellinc.com/beyond-machine-learning-and-ai-10x-faster-deployments-and-indico-4f412fd87b22

[^5]: https://10xdatascience.com

[^6]: https://deepsense.ai/case-studies/boosting-device-performance-by-10x-with-edge-ai-and-cv/

[^7]: https://blog.datagran.io/posts/data-science-10x-faster-with-ai

[^8]: https://epoch.ai/trends