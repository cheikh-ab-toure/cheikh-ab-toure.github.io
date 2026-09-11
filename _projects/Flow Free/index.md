---
layout: post
title: Investigating the Use of Machine Learning Algorithms to Solve Flow Free Puzzles
description:  A research project exploring machine learning methods, including a CNN-based MobileNetV2 model, to automatically solve Flow Free puzzles — with direct ties to circuit routing algorithms used in chip design.
skills: 
- Python
- OpenCV
- TensorFlow
- NumPy
main-image: /project.webp 
---

---
# Abstract
Routing is the process of selecting a path that connects two points while satisfying a set of constraints — a core problem in circuit design, including connecting logic gates on a chip. These same routing principles apply to Flow Free, a commercially available puzzle game with three constraints: dots of the same color must connect, lines cannot overlap, and every space must be filled.

As puzzle size increases, the computational complexity needed to solve it grows sharply. Traditional solvers struggle to keep up, so this research explores machine learning as an alternative approach — training a model to solve Flow Free automatically. I worked on this as part of a 7-member research team advised by Dr. Daniel Limbrick in the ADEPT Lab at NC A&T.

---
# How to Solve Flow Free
In Flow Free, the goal is to connect matching colored dots with continuous paths without violating game constraints. Multi-colored dot pairs are randomly placed on a 5x5 grid; connecting one pair incorrectly can block other paths and make the puzzle unsolvable.
Before turning to machine learning, we looked at three algorithmic approaches:
- Constraint Satisfaction & Backtracking — apply constraints, eliminate invalid moves, build a solution from remaining valid paths.
- Trial and Error Pathfinding — treat the puzzle like a maze, solving one color at a time, backing up whenever a path breaks a rule.
- SAT Solver — convert the puzzle into Boolean logic constraints, represent solutions as true/false combinations, and search for a satisfying assignment.

---
# Extracting Data with OpenCV
To train a model, we needed structured data extracted from puzzle images:
- OpenCV interprets images by detecting patterns, shapes, and colors, converting a screenshot into structured data for the model
- The board is isolated by detecting edges and contours, then divided into equal cells based on its dimensions
- Each cell is converted to HSV color space and classified as an endpoint, a path, or empty
- The result is compiled into a matrix representing the board's colors and states
  
{% include image-gallery.html images="extraction-pipeline-flowchart.png" height="450" %}
