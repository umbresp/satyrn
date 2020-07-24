[![Codacy Badge](https://app.codacy.com/project/badge/Grade/9b7ffe7dce94475e9fc5100096c3c8cf)](https://www.codacy.com/manual/CharlesAverill/satyrn?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=CharlesAverill/satyrn&amp;utm_campaign=Badge_Grade)
[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)
[![PyPI](https://img.shields.io/pypi/v/satyrn-python)](https://pypi.org/project/satyrn-python/)

[![GitHub license](https://img.shields.io/github/license/Naereen/StrapDown.js.svg)](https://github.com/CharlesAverill/satyrn/blob/master/LICENSE)
[![Open Source Love svg1](https://badges.frapsoft.com/os/v1/open-source.svg?v=103)](https://github.com/ellerbrock/open-source-badges/)


[![Maintenance](https://img.shields.io/badge/Maintained%3F-yes-green.svg)](https://GitHub.com/CharlesAverill/satyrn/graphs/commit-activity)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

[![GitHub issues](https://img.shields.io/github/issues/CharlesAverill/satyrn?label=open%20issues)](https://github.com/CharlesAverill/satyrn/issues)
[![GitHub issues-closed](https://img.shields.io/github/issues-closed-raw/CharlesAverill/satyrn?color=gree)](https://github.com/CharlesAverill/satyrn/issues?q=is%3Aissue+is%3Aclosed)

[![Say Thanks!](https://img.shields.io/badge/Say%20Thanks-!-1EAEDB.svg)](https://saythanks.io/to/charlesaverill20@gmail.com)

# Satyrn

![](satyrnCLI/media/cover.png?raw=true)
Satyrn is a command-line-based alternative to Jupyter notebooks.
The backend is completely based on node networks, because it supports branching, multithreaded cell paths.

This project is based on [this JEP](https://github.com/jupyter/enhancement-proposals/pull/50) for the Jupyter ecosystem. <s>I'm using this as a way to prepare for development of the features I've listed in the enhancement proposal.</s> The Satyrn team is developing a web-based UI.

## Setup
- Run `python -m pip install satyrn-python`
- Run `satyrnCLI` in your terminal to open the Satyrn CLI
- Run `satyrn` in your terminal to open the Satyrn UI (unstable)
- Code output from the Satyrn UI will appear in the terminal that the `satyrn` command was run from

## CLI Commands
* `quit` - Quits out of interpreter
* `cell [cell_name] [content_type](python/markdown) [add_content](y/n)`
    - Creates cell with given parameters
    - All cells require unique names
    - The first cell created will always be treated as the "root" cell, and will always be executed first in a complete execution call.
    - Set `content_type` to "python" for python cells
    - If `add_content` is "y", a text box will pop up. Input your python code here.
* `remove [cell_name]`
    - Deletes cell and its links from graph. 
* `edit [cell_name]`
    - Reopens text input window so that users can edit cells
* `link [first_cell_name] [second_cell_name]`
    - Links the two cells whose names are provided. You can technically still make branching graphs this way, but they
    will not work at all.
* `sever [first_cell_name] [second_cell_name]`
    - Severs the link between the two cells whose names are provided
* `merge [first_cell_name] [second_cell_name]`
    - Merges the two cells if they are adjacent.
* `swap [first_cell_name] [second_cell_name]`
    - Swaps the contents and names of the named cells. e.g. 
        - `a -> b -> c`
        - `swap a b`
        - `b -> a -> c`
* `execute [cell_name_1] [cell_name_2] ... >> (filename)`
    - If no cell names are defined, the entire graph will execute sequentially
    - If cell names are defined, they will execute in the order they are named
    - `>> (filename)` is optional. If included, will save stdout cell output to whatever filename is provided.
* `display [cell_name]`
    - If `cell_name` is defined, that cell's contents will be printed to the console
    - Otherwise, the entire graph will be displayed in matplotlib.
* `list`
    - Prints a list of all cell names and edge pairs in graph
* `reset_runtime`
    - Deletes all local variables created by cells.
* `reset_graph`
    - Deletes all cells and variables. Equivalent of restarting Satyrn session.
* `save [filename].satx`
    - Saves graph to .satx file.
* `[filename].satx`
    - This will run a .satx file. It's just a reformatted version of the normal Satyrn input. [This test file](satyrnCLI/examples/syntax_example.satx) shows the basic syntax rules.

## CLI Example
Here, code written in [ ] brackets was typed into the text box popup.
```
♄: create_cell root python y
[x = 10]
♄: create_cell mid python y
[x *= 22]
♄: create_cell bottom python y
[print(x)]
♄: link root mid
♄: link mid bottom
♄: execute
220
♄: quit
```
