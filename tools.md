---
layout: default  # Or another layout if you have one
title: Evaluation Tools
permalink: /tools/ 
---

# Convenient Tools

We provide 5 scripts to generate evaluation results:
- **Error Table**: A table of RMSE translation and rotation errors.
- **Error Distribution Heat Map**: A distribution plot of the RMSE translation and rotation errors of multiple runs to evaluate the robustness of a SLAM system.
- **Error with Time**: A figure that shows the pose errors in 6 axes evolving with time.
- **Stereo Reconstruction**: A 3D reconstruction using the estimated camera trajectory and the stereo depth.
- **Trajectory Plot**: A 3D plot of the estimated trajectory and GT trajectory.


The code of scripts can be found on the [GitHub page]()

## Result Format
To use the convenient tools, the SLAM format should be save as the following format:

```
# timestamp tx ty tz qx qy qz qw
1653050828.546086072922 -0.001770058525 0.000278359631 -0.000904943742 0.000068303926 0.000966903164 0.000076414040 0.999999527297
1653050828.595986366272 -0.003527211945 -0.000320959232 -0.001085915391 -0.000569093969 0.001472297661 0.000584394569 0.999998583476
1653050828.647124767303 -0.003186839487 0.000752073134 -0.000408260033 0.000436202469 0.000805340200 0.000511369736 0.999999449828
```

## File Structure
We follow the structure of [rpg_trajectory_evaluation](https://github.com/uzh-rpg/rpg_trajectory_evaluation) package.
To use the convenient tools, the SLAM pose file should be format as the following structure:

```
<platform>
├── <alg1>
│   ├── <platform>_<alg1>_<dataset1>
│   ├── <platform>_<alg1>_<dataset2>
│   └── ......
└── <alg2>
│   ├── <platform>_<alg2>_<dataset1>
│   ├── <platform>_<alg2>_<dataset2>
    ├── ......
......
```


# Evaluation Results
We evaluate the performance of four SLAM systems, i.e., [Underwater Visual Acoustic SLAM (UVA)](https://ieeexplore.ieee.org/document/9636258), [SVIN2](https://journals.sagepub.com/doi/full/10.1177/02783649221110259), [ORB SLAM3](https://ieeexplore.ieee.org/document/9440682) and [VINS-Fusion](https://github.com/HKUST-Aerial-Robotics/VINS-Fusion), on the proposed Tank dataset by reporting the generated results using the evaluation tool set.

## Error Table
The RMSE absolute errors are presented in following Table. UVA demonstrates the best performance in translation error across most sequences, attributed to the integration of the DVL. Regarding the rotation error, SVIN2 outperforms on less challenging sequences, while UVA excels in more challenging ones. ORB-SLAM3 performs well on the SE sequence but loses track in more challenging scenarios. VINS-Fusion also performs adequately on the SE sequence, but drifts rapidly in other sequences.

<table>
  <thead>
    <tr>
      <th></th>
      <th colspan="4">Translation Error (in meter)</th>
      <th colspan="4">Rotation Error (in degree)</th>
    </tr>
    <tr>
      <th>Sequence</th>
      <th>UVA</th>
      <th>SVIN2</th>
      <th>ORB3</th>
      <th>VINS</th>
      <th>UVA</th>
      <th>SVIN2</th>
      <th>ORB3</th>
      <th>VINS</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Structure Easy</td>
      <td>0.178</td>
      <td><strong>0.090</strong></td>
      <td>0.199</td>
      <td>0.219</td>
      <td>4.109</td>
      <td><strong>1.756</strong></td>
      <td>4.183</td>
      <td>2.321</td>
    </tr>
    <tr>
      <td>Structure Medium</td>
      <td><strong>0.489</strong></td>
      <td>2.111</td>
      <td>3.494</td>
      <td>42359.413</td>
      <td><strong>10.982</strong></td>
      <td>57.510</td>
      <td>90.014</td>
      <td>65.957</td>
    </tr>
    <tr>
      <td>Structure Hard</td>
      <td><strong>0.432</strong></td>
      <td>3.589</td>
      <td>2.933</td>
      <td>5165.797</td>
      <td><strong>5.923</strong></td>
      <td>23.439</td>
      <td>102.615</td>
      <td>38.244</td>
    </tr>
    <tr>
      <td>HalfTank Easy</td>
      <td><strong>1.121</strong></td>
      <td>4.508</td>
      <td>2.213</td>
      <td>26.930</td>
      <td>19.827</td>
      <td><strong>3.456</strong></td>
      <td>48.613</td>
      <td>8.435</td>
    </tr>
    <tr>
      <td>HalfTank Medium</td>
      <td><strong>0.256</strong></td>
      <td>2.902</td>
      <td>0.708</td>
      <td>15772.612</td>
      <td><strong>5.935</strong></td>
      <td>24.153</td>
      <td>15.159</td>
      <td>45.991</td>
    </tr>
    <tr>
      <td>HalfTank Hard</td>
      <td><strong>0.367</strong></td>
      <td>68.703</td>
      <td>1.147</td>
      <td>31722.982</td>
      <td><strong>9.850</strong></td>
      <td>15.647</td>
      <td>22.236</td>
      <td>92.070</td>
    </tr>
    <tr>
      <td>WholeTank Medium</td>
      <td><strong>0.267</strong></td>
      <td>0.406</td>
      <td>0.682</td>
      <td>4.106</td>
      <td>9.202</td>
      <td><strong>6.578</strong></td>
      <td>8.195</td>
      <td>91.497</td>
    </tr>
    <tr>
      <td>WholeTank Hard</td>
      <td>0.297</td>
      <td><strong>0.274</strong></td>
      <td>2.370</td>
      <td>35999.266</td>
      <td>10.697</td>
      <td><strong>3.796</strong></td>
      <td>30.504</td>
      <td>28.585</td>
    </tr>
  </tbody>
</table>


## Error Distribution Heat Map
The error distribution heat map, presented in the following figure, illustrates the error deviations across 10 runs for each method. The UVA method demonstrates the highest robustness across the majority of the sequences.
![error_map_t]({{ site.baseurl }}/images/slam_error_map_rmse_t.png)
![error_map_r]({{ site.baseurl }}/images/slam_error_map_rmse_r.png)

For more results, please refer to our [paper]().