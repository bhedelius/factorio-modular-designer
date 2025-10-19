# Factorio modular designer

This project creates diagrams of the number of items and machines required to make certain products in factorio. This should make it easier to create blueprints for certain products, make builds more modular.

So far my work is in the factorio_modular_designer.ipynb file. It creates png files in the output directory. The png files displays the item icons as well as the number of items per second and machines rquired. They also shows downstream how those items should be directed, the arrows between items show the ratio of input to output machines and how many items go towards a certain product.

There are constants at the top of the file to change the speeds if using different assemblers or furnaces. You can also change the product by changing the code in the last block.

This project is rough and doesn't have a great user experience (I'm mainly building this for myself right now since I didn't find a tool that did what I wanted). If you are interested in using this as a tool, I'd be happy to create a more accessible notebook in colab, just contact me at bhedelius@gmail.com.

The notes.txt file is a list of things I want to work on next to improve this and things I want to remember
