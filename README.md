# Divergent Tastes: Mapping the Cultural Distance Between Pitchfork and Billboard (2015–2024)

## Research Goal:
This project investigates how musical reputation is shaped through two distinct lenses—critical acclaim (Pitchfork) and mainstream popularity (Billboard). Through artist frequency, genre presence, temporal patterns, and thematic content, we explore where these two platforms align and diverge in their musical valuation.

## 1. Overview of Alignment and Divergence

Drake and Kendrick Lamar are the clearest cross-platform outliers, topping both Pitchfork and Billboard charts consistently from 2015 to 2024. This suggests a rare convergence of critical and commercial success.

Other artists like Ariana Grande, Taylor Swift, and The Weeknd dominated Billboard lists but had significantly less presence on Pitchfork, highlighting a bias toward pop accessibility over critical edge.

In contrast, Charli XCX, Frank Ocean, Angel Olsen, and Moses Sumney received repeated Pitchfork recognition but were largely absent from Billboard’s top ranks—indicating a critical preference for sonic experimentation and conceptual depth.

![Alt Text](docs/overall.png)



## 2. Year-Specific Divergences (e.g., 2016, 2024)

In 2016, Billboard spotlighted The Weeknd, Adele, and Shawn Mendes, while Pitchfork favored Chance the Rapper, Frank Ocean, and Kanye West. The contrast reflects differing reactions to genre fluidity and artistic boldness.

In 2024, the gap widened: Pitchfork recognized experimental or niche artists such as Mach-Hommy and evilgiane, while Billboard featured more mainstream figures like Billie Eilish and Sabrina Carpenter.



## 3. Temporal Trends (2015–2024)

Billboard’s top mentions over the decade:
• Drake, Ariana Grande, and Taylor Swift dominate with 20+ mentions.

Pitchfork’s top mentions:
• More evenly distributed, with Kendrick Lamar and Drake at the top (10 mentions), and a wider spread among indie and alternative acts.

This distribution reveals Billboard’s loyalty to chart-topping consistency, while Pitchfork spreads attention across more artists, reflecting evolving editorial interests.

### Billboard V.S. Pitchfork:
Overall
![Alt Text](docs/pitchfork_2015_2024.png)
![Alt Text](docs/billboard_2015_2024.png)

2015
![Alt Text](docs/pitchfork_2015.png)
![Alt Text](docs/billboard_2015.png)

2016
![Alt Text](docs/pitchfork_2016.png)
![Alt Text](docs/billboard_2016.png)

2017
![Alt Text](docs/pitchfork_2017.png)
![Alt Text](docs/billboard_2017.png)

2018
![Alt Text](docs/pitchfork_2018.png)
![Alt Text](docs/billboard_2018.png)

2019
![Alt Text](docs/pitchfork_2019.png)
![Alt Text](docs/billboard_2019.png)

2020
![Alt Text](docs/pitchfork_2020.png)
![Alt Text](docs/billboard_2020.png)

2021
![Alt Text](docs/pitchfork_2021.png)
![Alt Text](docs/billboard_2021.png)

2022
![Alt Text](docs/pitchfork_2022.png)
![Alt Text](docs/billboard_2022.png)

2023
![Alt Text](docs/pitchfork_2023.png)
![Alt Text](docs/billboard_2023.png)

2024
![Alt Text](docs/pitchfork_2024.png)
![Alt Text](docs/billboard_2024.png)


# songs_in_both_table.py

import pandas as pd
import plotly.graph_objects as go
from IPython.display import display, HTML

# Load data
df = pd.read_csv("merged_2015_2024_with_wiki_images.csv")

# Filter songs with both Pitchfork and Billboard ranks
songs_in_both = df.dropna(subset=['pitchfork_rank', 'billboard_rank']).copy()
songs_in_both['pitchfork_rank'] = songs_in_both['pitchfork_rank'].astype(int)
songs_in_both['billboard_rank'] = songs_in_both['billboard_rank'].astype(int)
songs_in_both['average_rank'] = ((songs_in_both['pitchfork_rank'] + songs_in_both['billboard_rank']) / 2).round(1)

result_df = songs_in_both[['year', 'artists', 'song', 'pitchfork_rank', 'billboard_rank', 'average_rank', 'image']]

# Generate HTML with hoverable image preview
html = '''
<style>
  body { background-color: #000; color: #fff; font-family: 'Courier New', monospace; }
  table { width: 100%; border-collapse: collapse; background: rgba(255,255,255,0.1); }
  th, td { padding: 10px; border-bottom: 1px solid rgba(255,255,255,0.2); text-align: left; font-family: 'Courier New', monospace; }
  th { background: rgba(255,255,255,0.2); }
  tr:hover { background-color: rgba(255, 255, 255, 0.3); }
  .preview-img { position: absolute; left: calc(100% - 240px); top: 0; display: none; width: 200px; border-radius: 12px; box-shadow: 0 0 20px rgba(255,255,255,0.3); z-index: 100; }
</style>
<h2>Songs Ranked on Both Pitchfork and Billboard</h2>
<table id="rank-table">
  <thead>
    <tr>
      <th>Year</th>
      <th>Artist</th>
      <th>Song</th>
      <th>Pitchfork Rank</th>
      <th>Billboard Rank</th>
      <th>Average Rank</th>
    </tr>
  </thead>
  <tbody>
'''

for i, row in result_df.iterrows():
    image_url = row['image'].replace('"', '')
    html += f'''
    <tr onmousemove="const img=document.getElementById('hover-img'); img.src='{image_url}'; img.style.top=event.clientY+'px'; img.style.display='block';" 
        onmouseleave="document.getElementById('hover-img').style.display='none';">
      <td>{row['year']}</td>
      <td>{row['artists']}</td>
      <td>{row['song']}</td>
      <td>{row['pitchfork_rank']}</td>
      <td>{row['billboard_rank']}</td>
      <td>{row['average_rank']}</td>
    </tr>
    '''

html += '''</tbody></table><img id="hover-img" class="preview-img" />'''

# Display the interactive table
display(HTML(html))



## 4. Cultural Distance in Taste & Values

Pitchfork prioritizes:
 • Innovation, genre blending, emotional intimacy, cultural critique
 • Artists who take risks or push boundaries

Billboard prioritizes:
 • Broad appeal, streaming metrics, radio play, and viral trends
 • Artists with sustained media presence and label support


## 5. Implications

The critical-popular divide isn’t just about taste—it reveals different logics of value: artistic depth vs. market traction.

Artists who bridge both (e.g., Kendrick, Frank Ocean, Billie Eilish) are rare and culturally significant because they navigate both spheres successfully.

For artists and producers, this duality underscores the challenge: Do you want critical legacy or mass reach? Often, they are not the same path.


## 6. Conclusion

Pitchfork and Billboard offer two distinct cultural lenses. Understanding their divergences isn’t just about music—it’s a study in how culture is validated, by either curators or consumers. By mapping the patterns over a decade, this project lays the groundwork for analyzing future shifts in musical value systems—especially as the boundary between underground and mainstream continues to blur in the age of streaming and algorithmic discovery.