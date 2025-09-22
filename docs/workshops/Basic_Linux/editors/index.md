# Text Editors on Linux

=== "Nano"

    Nano is a straightforward and user-friendly text editor, making it a great choice for beginners.

    - Opening a file

        ```bash
        nano filename.txt
        ```

    - Basic Commands

        | Command    |  Description |          
        | -------    | ------------ |
        | Type       |   Edit text directly                           | 
        | `Ctrl + O` |   Save changes                                 |
        | `Ctrl + X` |   Exit the editor (prompt to save if needed)   |
        | `Ctrl + K` |   Cut the current line                         |
        | `Ctrl + U` |   Paste the cut line                           | 
        | `Ctrl + W` |   Search for text                              |
        | Arrow keys |   Navigate through the text                    |


=== "Vim/Vi"

    Vim (Vi IMproved) is a powerful text editor that is widely used in the Linux environment. It operates in different modes, primarily **Normal**, **Insert**, and **Visual** modes.

    - Opening a File

        ```bash
        vi filename.txt
        ```

    - Basic Commands in **Normal Mode**

        | Command      |   Description                                     |
        | ---------    | ------------------------------------------------- |
        | i            |  Switch to Insert mode                            |
        | a            |  Switch to Insert mode (append)   |
        | v            |  Switch to Visual mode             |
        | :w           |  Save changes     |
        | :wq          |  Save and exit  |
        | :q!          |  Exit without saving  |
        | h, j, k, l   |  Navigate left, down, up, and right, respectively | 
        | dd           |  Delete the current line   |
        | u            |  Undo the last action   | 
    

    !!! info "You can exit from **Insert Mode** by hitting ESC key. It will change the status to **Normal Mode**"
