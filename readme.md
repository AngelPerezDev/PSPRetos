<h1 id="what-is-markdown">What is Markdown?</h1>
      <blockquote>
      <p>Markdown is a text-to-HTML conversion tool for web writers. Markdown allows you to write using an easy-to-read, easy-to-write plain text format, then convert it to structurally valid XHTML (or HTML).</p>
      </blockquote>
      <p>Source: <a href="http://daringfireball.net/projects/markdown/">http://daringfireball.net/projects/markdown/</a></p>
      <h1 id="installation">Installation</h1>
      <p>The plugin is <a href="http://plugins.netbeans.org/plugin/50964/markdown-support">available</a> in the official NetBeans Plugin Portal Update Center.</p>
      <p>You can also download a pre-packaged release:</p>
      <ul>
      <li>https://github.com/madflow/flow-netbeans-markdown/releases (list of all releases)</li>
      <li>https://github.com/madflow/flow-netbeans-markdown/releases/download/2.3.1/flow-netbeans-markdown.nbm (<strong>note:</strong> version 2.3.1)</li>
      </ul>
      <p>Install the plugin with: <code>Tools -&gt; Plugins -&gt; Downloaded</code></p>
      <p>You may also compile a binary yourself with the <strong>latest development code</strong>.</p>
      <ol>
      <li>git clone git://github.com/madflow/flow-netbeans-markdown.git</li>
      <li>Open the folder with NetBeans (Open Project)</li>
      <li>(Configure Target Platform if needed)</li>
      <li>Choose &quot;Create NBM&quot; from the project menu</li>
      <li>Install the plugin with: Tools -&gt; Plugins -&gt; Downloaded</li>
      </ol>
      <h1 id="requirements">Requirements</h1>
      <ul>
      <li>NetBeans &gt;= 8.0</li>
      <li>&quot;NetBeans Plugin Development&quot; plugin must be installed if you want to compile your own binary package.</li>
      </ul>
      <h1 id="plugin-features">Plugin features</h1>
      <ul>
      <li>Adds Markdown to your &quot;New File&quot; wizard</li>
      <li>Provides basic syntax highlighting</li>
      <li>Provides code folding based on headers</li>
      <li>Provides bread crumbs in the editor based on headers</li>
      <li>Provides a table of contents in the Navigator window</li>
      <li>Enables full fledged preview in the editor window</li>
      <li>Exports your saved file content to an HTML document</li>
      <li>Enables HTML preview of your saved file in your configured web browser</li>
      <li>Lets you customize the HTML output with CSS and alien intelligence (Options-&gt;Miscellaneous-&gt;Markdown-&gt;HTML Export)</li>
      <li>Supports multiple extensions over standard markdown (see <a href="https://github.com/sirthias/pegdown">PegDown</a>, Options-&gt;Miscellaneous-&gt;Markdown-&gt;Extensions)</li>
      <li>Supports auto operations(additoin and removal) for lists (Options-&gt;Miscellaneous-&gt;Markdown-&gt;Miscellaneous)</li>
      </ul>
      <h1 id="screenshots">Screenshots</h1>
      <p><img src="editor-source.png" alt="Editor - Source view" title="The Source view of the Markdown editor"></p>
      <hr>
      <p><img src="editor-preview.png" alt="Editor - Preview view" title="The Preview view of the Markdown editor"></p>
      <h1 id="resources">Resources</h1>
      <ul>
      <li><a href="https://github.com/sirthias/pegdown">PegDown</a> : A pure-Java Markdown processor based on a parboiled PEG parser supporting a number of extensions.</li>
      <li>http://daringfireball.net/projects/markdown/ : Home of the Markdown (Basics, Syntax)</li>
      <li>http://openiconlibrary.sourceforge.net/ : Icons</li>
      <li><a href="http://dcurt.is/the-markdown-mark">Markdown Mark</a> : A graphic element to identify Markdown files created by <a href="http://dustincurtis.com/">Dustin Curtis</a> (<a href="https://github.com/dcurtis/markdown-mark">Github repo</a>)</li>
      </ul>
