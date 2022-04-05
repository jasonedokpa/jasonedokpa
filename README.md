### Hi there 👋

<!--
**jasonedokpa/jasonedokpa** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- ⚡ Fun fact: ...
-->


<div id="header" align="center">
  <img src="https://media.giphy.com/media/M9gbBd9nbDrOTu1Mqx/giphy.gif" width="100"/>
</div>


<body><div id="MathJax_Message" style="display: none;"></div><script>sshowControl0 = { counter: 1,
             showNumber: 0, max: 1};
             window.onhashchange = hashHasChanged;</script><div class="navHeader" id="slideshowControlA0"><table class="navHeader"><tbody><tr class="slideshowcontrol"><td class="slideshowcontrolLeft"></td><td class="slideshowcontrolMiddle">
<a class="imgLink" href="../../Directory/outline/index.html" title="Course home/outline"><img src="../../graphics/home.png"></a>
<a href="mailto:tkennedy@cs.odu.edu?subject=CS330%2C%20Asst%3A%20Item%20Inventory"><img src="../../graphics/email.png" title="Email to instructor"></a><span style="margin: 0 32px;"></span></td><td class="slideshowcontrolRight"></td></tr></tbody></table></div><div class="mainBody"><div class="titleblock"><h1 class="title">Asst: Item Inventory</h1><h2 class="author">Thomas Kennedy</h2></div><div class="toc">Contents:<div class="toc-h1"><a href="#design-and-s-o-l-i-d">1 Design and S.O.L.I.D</a></div><div class="toc-h1"><a href="#the-problem">2 The Problem</a></div><div class="toc-h2"><a href="#input">2.1 Input</a></div><div class="toc-h2"><a href="#output">2.2 Output</a></div><div class="toc-h2"><a href="#running-the-program">2.3 Running the Program</a></div><div class="toc-h2"><a href="#your-tasks">2.4 Your Tasks</a></div><div class="toc-h1"><a href="#hints">3 Hints</a></div><div class="toc-h1"><a href="#mechanics">4 Mechanics</a></div><div class="toc-h2"><a href="#grading-tests">4.1 Grading &amp; Tests</a></div><div class="toc-h2"><a href="#files">4.2 Files</a></div><div class="toc-h2"><a href="#submitting">4.3 Submitting</a></div></div><p>Read these <a class="doc" href="../../Public/submitting/index.html" target="CS330_Public">general instructions on turning in assignments</a>  for this course.</p>
    <a id="designandsolid"><h1 id="design-and-s-o-l-i-d">1 Design and S.O.L.I.D</h1><p>The code in this assignment violates a number of best practices…</p>
    <ol>
  <li>S.O.L.I.D</li>
  <li>D.R.Y</li>
  <li>Abuse of inline functions</li>
  <li>No use of Constructor Delegation in <code>Inventory</code></li>
  <li><em>Data Structure Logic</em> is merged with <em>Business Logic</em></li>
</ol><p>However, we have to start somewhere. These terms and best practices will be discussed starting in Review 02. <em>The next Assignment will be a lot more fun!</em></p>
    <hr></a><a id="theproblem"><h1 id="the-problem">2 The Problem</h1></a><p><a id="theproblem">This assignment deals with a program places items into separate inventories. This is similar to placing items into chests in </a><a href="https://minecraft.net/">Minecraft</a>.</p>
    <h2 id="input">2.1 Input</h2><p>The program reads data from two files, <em>itemsList-0x.txt</em> and <em>inventoryList-0x.txt</em>. File extensions on Linux may be arbitrary–i.e., these files could have been named with <em>.dat</em> as the extensions.</p>
    <p>The first file, <em>itemsList-0x.txt</em>, lists all possible items. Each line represents one item in the form <em>id name</em>.</p>
    <blockquote class="example" id="example1"><div class="exampleTitle">Example 1: Sample itemsList-0x.txt</div>
<pre><code class=" hljs ">0 Air
1 HP Potion
2 MP Potion
5 Iron Ore
3 Bow Tie
4 Dirt
6 Diamond Ore
7 Iron Ingot
8 Diamond
9 Diamond Block
</code></pre>
</blockquote><p>The second file, <em>inventoryList-0x.txt</em>, lists each individual inventory–or storage chest–followed by a list of items.</p>
    <blockquote class="example" id="example2"><div class="exampleTitle">Example 2: Sample inventoryList-0x.txt</div>
<pre><code class=" hljs markdown"><span class="hljs-header"># 5</span>
<span class="hljs-bullet">- </span>1 10
<span class="hljs-bullet">- </span>2  5
<span class="hljs-bullet">- </span>3  2
<span class="hljs-header"># 6</span>
<span class="hljs-bullet">- </span>4  3
<span class="hljs-bullet">- </span>5 27
<span class="hljs-bullet">- </span>6 44
<span class="hljs-bullet">- </span>7 55
<span class="hljs-bullet">- </span>8  1
<span class="hljs-bullet">- </span>9  4
<span class="hljs-bullet">- </span>4  3
<span class="hljs-header"># 2</span>
<span class="hljs-bullet">- </span>2  5
<span class="hljs-bullet">- </span>9  4
<span class="hljs-bullet">- </span>8  1
<span class="hljs-bullet">- </span>5  2
<span class="hljs-bullet">- </span>10 5
</code></pre>
</blockquote><p>Each line preceded by <em>#</em> denotes the start of a new inventory. Each line preceded by <em>-</em> denotes an item. The program creates a new inventory each time a <em>#</em> is encountered.</p>
    <p>When a <em>-</em> is encountered, a stack of items, ItemStack, is created. The <em>ItemStack</em> is placed in the <em>Inventory</em> based on the following rules:</p>
    <ol>
  <li>If the Inventory is empty, store the ItemStack, and <code>return true</code>.</li>
  <li>If the Inventory is not empty, examine the Inventory.
    <ul>
      <li>If a matching ItemStack is found, merge the two ItemStacks and <code>return
  true</code>.</li>
      <li>If no matching ItemStack is found, store the new ItemStack and <code>return
  true</code>.</li>
    </ul>
  </li>
  <li>If the Inventory is full, <code>return false</code>.</li>
</ol><p>Through the magic of abstraction, this is not one function, but four (4) functions in total. Yes, it does seem unnecessary at first. However, each function does one thing and only one thing. This is an exercise in understanding the thought process behind abstraction, interfaces, and the <code>S</code>/<code>O</code> in <code>S.O.L.I.D</code> (with some C++ code) in a multi-ADT program.</p>
    <p>Most of your time will be spent on understanding the abstractions (and interfaces) as opposed to spamming cobblestone blocks… I mean C++ code.</p>
    <h2 id="output">2.2 Output</h2><p>The output consists of three reports written to standard output, one after the other.</p>
    <ol>
  <li>
  <p>A report listing items that were stored or discarded.</p>
    </li>
  <li>
  <p>A report listing all valid items.</p>
    </li>
  <li>
    <p>Finally, a detailed report is printed. listing data for each inventory:</p>
    
    <ul>
      <li>Maximum Capacity–i.e., total slots.</li>
      <li>Utilized Capacity–i.e., occupied slots</li>
      <li>Listing of all items.</li>
    </ul>
  </li>
</ol><p>If the program is run with the provided input files, the following output should be generated…</p>
    <blockquote class="example" id="example3"><div class="exampleTitle">Example 3: Sample Output</div>
<pre><code class=" hljs php">Processing Log:
 Stored (<span class="hljs-number">10</span>) HP Potion
 Stored ( <span class="hljs-number">5</span>) MP Potion
 Stored ( <span class="hljs-number">2</span>) Bow Tie
 Stored ( <span class="hljs-number">3</span>) Dirt
 Stored (<span class="hljs-number">27</span>) Iron Ore
 Stored (<span class="hljs-number">44</span>) Diamond Ore
 Stored (<span class="hljs-number">55</span>) Iron Ingot
 Stored ( <span class="hljs-number">1</span>) Diamond
 Stored ( <span class="hljs-number">4</span>) Diamond Block
 Stored ( <span class="hljs-number">3</span>) Dirt
 Stored ( <span class="hljs-number">5</span>) MP Potion
 Stored ( <span class="hljs-number">4</span>) Diamond Block
 Discarded ( <span class="hljs-number">1</span>) Diamond
 Discarded ( <span class="hljs-number">2</span>) Iron Ore

Item <span class="hljs-keyword">List</span>:
   <span class="hljs-number">0</span> Air
   <span class="hljs-number">1</span> HP Potion
   <span class="hljs-number">2</span> MP Potion
   <span class="hljs-number">3</span> Bow Tie
   <span class="hljs-number">4</span> Dirt
   <span class="hljs-number">5</span> Iron Ore
   <span class="hljs-number">6</span> Diamond Ore
   <span class="hljs-number">7</span> Iron Ingot
   <span class="hljs-number">8</span> Diamond
   <span class="hljs-number">9</span> Diamond Block

Storage Summary:
 -Used <span class="hljs-number">3</span> of <span class="hljs-number">5</span> slots
  (<span class="hljs-number">10</span>) HP Potion
  ( <span class="hljs-number">5</span>) MP Potion
  ( <span class="hljs-number">2</span>) Bow Tie

 -Used <span class="hljs-number">6</span> of <span class="hljs-number">6</span> slots
  ( <span class="hljs-number">6</span>) Dirt
  (<span class="hljs-number">27</span>) Iron Ore
  (<span class="hljs-number">44</span>) Diamond Ore
  (<span class="hljs-number">55</span>) Iron Ingot
  ( <span class="hljs-number">1</span>) Diamond
  ( <span class="hljs-number">4</span>) Diamond Block

 -Used <span class="hljs-number">2</span> of <span class="hljs-number">2</span> slots
  ( <span class="hljs-number">5</span>) MP Potion
  ( <span class="hljs-number">4</span>) Diamond Block

</code></pre>
</blockquote><a id="runningtheprogram"><h2 id="running-the-program">2.3 Running the Program</h2><p>The easiest way to see generate the expected output is to run the sample executable solution I have provided. These two files are named as command-line parameters when the program is executed.</p>
    <p>For example, if the sample data above is kept in files itemList-01.txt and inventoryList-01.txt, then to run this program, do:</p>
    <pre><code class="sh hljs ">./storage itemList-01.txt inventoryList-01.txt
</code></pre></a><p><a id="runningtheprogram">(On a Windows system, you would omit the “./”. If you are running from Code::Blocks or a similar development environment, you may need to review how to </a><a href="https://www.cs.odu.edu/~zeil/cs333/latest/Public/supplyingInputsLab/">supply command-line parameters</a> to a running program.)</p>
    <a id="yourtasks"><h2 id="your-tasks">2.4 Your Tasks</h2><p>The key abstractions employed in this program are <em>Inventory</em>, <em>Item</em>, and <em>ItemStack</em>. Complete ADT implementations have been provided for the latter two.</p>
    <p>The <em>Inventory</em> class is partially implemented. Your task is to complete the Inventory ADT. The code provided will not run correctly… until you complete all the following methods:</p>
    <ol>
  <li>Copy Constructor</li>
  <li>Destructor</li>
  <li>Assignment Operator
    <ul>
      <li>Note this is already provided and complete. Refer to our  discussions of the copy-and-swap method.</li>
      <li>Once you have completed the Copy Constructor and Destructor,  you are done with the Big-3.</li>
    </ul>
  </li>
  <li><code>Inventory::isFull</code> - refer to documentation in Inventory.h.</li>
  <li><code>Inventory::findMatchingItemStackNode</code> - refer to documentation in Inventory.h.</li>
  <li><code>Inventory::mergeStacks</code> - refer to documentation in Inventory.h.</li>
  <li><code>Inventory::addItemStackNoCheck</code> - refer to documentation in Inventory.h.</li>
</ol><p>The partial implementation provided assumes that each Inventory will keep track of items in a linked list. You must <strong>not</strong> change this choice of data structure… <strong>unless you want a zero.</strong></p>
    </a><a id="checkingformemoryleaks"><h3 id="checking-for-memory-leaks">2.4.1 Checking for Memory Leaks</h3></a><p><a id="checkingformemoryleaks">As an aid to getting this program working correctly, the program has been instrumented with the compiler flag <code>-fsanitize=leak,address</code> detect memory leaks and other (selected) memory allocation problems. To see the memory usage report, compile your code on one of our Linux servers using the provided <code>makefile</code>, then run your program </a><a href="#running-the-program">as described above</a>.</p>
    <p>If your output is followed by</p>
    <pre><code class=" hljs javascript">==<span class="hljs-number">32194</span>==ERROR: LeakSanitizer: detected memory leaks

Direct leak of <span class="hljs-number">96</span> byte(s) <span class="hljs-keyword">in</span> <span class="hljs-number">3</span> object(s) allocated from:
    #<span class="hljs-number">0</span> <span class="hljs-number">0x7f92839b59f8</span> <span class="hljs-keyword">in</span> operator <span class="hljs-keyword">new</span>(unsigned long) (<span class="hljs-regexp">/usr/</span>lib/x86_64-linux-gnu/liblsan.so<span class="hljs-number">.0</span>+<span class="hljs-number">0xf9f8</span>)
    #<span class="hljs-number">1</span> <span class="hljs-number">0x406215</span> <span class="hljs-keyword">in</span> Inventory::addItemStackNoCheck(ItemStack) /home/tkennedy/not/real/inventory_llist/Solution/Inventory.cpp:<span class="hljs-number">131</span>
    #<span class="hljs-number">2</span> <span class="hljs-number">0x402370</span> <span class="hljs-keyword">in</span> Inventory::addItems(ItemStack) (<span class="hljs-regexp">/home/</span>tkennedy/not/real/inventory_llist/Solution/storage+<span class="hljs-number">0x402370</span>)
    #<span class="hljs-number">3</span> <span class="hljs-number">0x401dc2</span> <span class="hljs-keyword">in</span> parseInventoryFile(std::istream&amp;, std::vector&lt;Item, std::allocator&lt;Item&gt; &gt; <span class="hljs-keyword">const</span>&amp;) /home/tkennedy/not/real/inventory_llist/Solution/storage.cpp:<span class="hljs-number">165</span>
    #<span class="hljs-number">4</span> <span class="hljs-number">0x401913</span> <span class="hljs-keyword">in</span> main /home/tkennedy/not/real/inventory_llist/Solution/storage.cpp:<span class="hljs-number">90</span>
    #<span class="hljs-number">5</span> <span class="hljs-number">0x7f92830d0f44</span> <span class="hljs-keyword">in</span> __libc_start_main (<span class="hljs-regexp">/lib/</span>x86_64-linux-gnu/libc.so<span class="hljs-number">.6</span>+<span class="hljs-number">0x21f44</span>)

Direct leak of <span class="hljs-number">96</span> byte(s) <span class="hljs-keyword">in</span> <span class="hljs-number">3</span> object(s) allocated from:
    #<span class="hljs-number">0</span> <span class="hljs-number">0x7f92839b59f8</span> <span class="hljs-keyword">in</span> operator <span class="hljs-keyword">new</span>(unsigned long) (<span class="hljs-regexp">/usr/</span>lib/x86_64-linux-gnu/liblsan.so<span class="hljs-number">.0</span>+<span class="hljs-number">0xf9f8</span>)
    #<span class="hljs-number">1</span> <span class="hljs-number">0x406215</span> <span class="hljs-keyword">in</span> Inventory::addItemStackNoCheck(ItemStack) /home/tkennedy/not/real/inventory_llist/Solution/Inventory.cpp:<span class="hljs-number">131</span>
    #<span class="hljs-number">2</span> <span class="hljs-number">0x405fb4</span> <span class="hljs-keyword">in</span> Inventory::Inventory(Inventory <span class="hljs-keyword">const</span>&amp;) /home/tkennedy/not/real/inventory_llist/Solution/Inventory.cpp:<span class="hljs-number">52</span>
    #<span class="hljs-number">3</span> <span class="hljs-number">0x40208b</span> <span class="hljs-keyword">in</span> printInventories(std::vector&lt;Inventory, std::allocator&lt;Inventory&gt; &gt; <span class="hljs-keyword">const</span>&amp;) /home/tkennedy/not/real/inventory_llist/Solution/storage.cpp:<span class="hljs-number">198</span>
    #<span class="hljs-number">4</span> <span class="hljs-number">0x401968</span> <span class="hljs-keyword">in</span> main /home/tkennedy/not/real/inventory_llist/Solution/storage.cpp:<span class="hljs-number">94</span>
    #<span class="hljs-number">5</span> <span class="hljs-number">0x7f92830d0f44</span> <span class="hljs-keyword">in</span> __libc_start_main (<span class="hljs-regexp">/lib/</span>x86_64-linux-gnu/libc.so<span class="hljs-number">.6</span>+<span class="hljs-number">0x21f44</span>)

</code></pre><p>or something similar. You have a memory leak. Follow the steps I followed in <a class="doc" href="../../Protected/Reviews330/index.html" target="CS330_Protected">Review-01 Example 4</a>.</p>
    <p>If you see only the normal output (i.e., the 3 reports described previously), you have no memory leaks.</p>
    <h1 id="hints">3 Hints</h1><p>There are a few hints avalable <a href="./hints.mmd.html">here</a>.</p>
    <h1 id="mechanics">4 Mechanics</h1><a id="gradingtests"><h2 id="grading-tests">4.1 Grading &amp; Tests</h2><p>Grading for this assignment will be as follows:</p>
    <ul>
  <li>
  <p>Submitting code that compiles and links properly: 10%</p>
    </li>
  <li>
  <p>Program produces correct report output (exact match to my solution):  45%. <em>Note that I am forcing you to practice your head-to-head testing  from CS 250. You have my compiled solution, and input.</em></p>
    </li>
  <li>
  <p>Program produces correct report output with no reported memory leaks or other error messages: 45%</p>
    </li>
</ul><p>In the grade report that you receive, you will see tests numbered 000, 001, etc. The even numbered tests check the report output. The odd-numbered tests check for memory errors on the same input.</p>
    </a><a id="whereisthepartialcredit"><h3 id="where-is-the-partial-credit-">4.1.1 Where is the Partial Credit?</h3><p><strong>Everything in this assignment is a System Test.</strong> I am particularly persnickety with the grading for this exercise. <strong>Every function in this assignment is based on concepts and mechanics covered in CS 250.</strong></p>
    <p><strong>The overall goal of this assignment is to force you to reinforce your CS 250 foundations, during the first few weeks of the semester.</strong> If you run into issues, have questions, or are not sure where to start… come to office hours… or send me an email.</p>
    <h2 id="files">4.2 Files</h2></a><p><a id="whereisthepartialcredit">Files for this assignment appear in </a><a href="./Public">this directory</a> or, if you are logged in to a CS Dept Linux server, in <code>~tkennedy/Assignments/cs330/inventory_llist</code>.</p>
    <h2 id="submitting">4.3 Submitting</h2><p>Files to Submit:</p>
    <ul>
  <li>Inventory.cpp–i.e., your version of the Inventory ADT Implementation.</li>
</ul><p>Your submitted code must compile correctly–on our Linux servers (<code>atria.cs.odu.edu</code> and <code>sirius.cs.odu.edu</code>) with the other code (as provided), using the compilation commands generated by the provided makefile. Do not alter any of the other source code files, nor change the Inventory interface in such a way that it can only be compiled with some other compiler or some other sequence of commands.</p>
    <a id="submissionbutton"><h3 id="submission-button">4.3.1 Submission Button</h3><p>To submit your assignment, use the button below. You will receive a preliminary grade via email (to your ODU email account) and will also be able to check your grade from the course web page <em>Grades</em> button.</p>
    <form><div><input onclick="window.open('https://www.cs.odu.edu/~zeil/submit/submit.html?asstinfo=/home/tkennedy/Courses/Websites/cs330//s22/Assts/inventory_llist/inventory_llist.ini')" type="button" value="Submit this assignment"></div>
    </form></a></div><script>sshowControl0 = { counter: 1,
             showNumber: 0, max: 1};
             window.onhashchange = hashHasChanged;</script><div class="navFooter" id="slideshowControl0"><table class="navFooter"><tbody><tr class="slideshowcontrol"><td class="slideshowcontrolLeft"></td><td class="slideshowcontrolMiddle">
<a class="imgLink" href="../../Directory/outline/index.html" title="Course home/outline"><img src="../../graphics/home.png"></a>
<a href="mailto:tkennedy@cs.odu.edu?subject=CS330%2C%20Asst%3A%20Item%20Inventory"><img src="../../graphics/email.png" title="Email to instructor"></a><span style="margin: 0 32px;"></span></td><td class="slideshowcontrolRight"></td></tr></tbody></table></div><div class="copyright"><a id="submissionbutton">© 2015-2022, Old Dominion Univ.</a></div><a id="submissionbutton">
</a><iframe src="about:blank" style="display: none;"></iframe></body>
