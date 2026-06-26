# 6/11 Lecture: CS585 — Database Connectivity (Chapter 14)

### Cheatsheet-style lecture notes

> **One-line thesis:** *It's always the same picture* — a **client** talks to a **database** through a **middleware**. Over 30 years only the **names of the layers** change. **Nothing is ever thrown away; we only add layers on top.** (Same reason "nothing in Agents / MCP is truly new.")

------

## 1. The Big Picture — 3-Tier (and 4-Tier) Architecture

Every app you touch (DoorDash, Uber, Subway, even a game leaderboard) is talking to a **database**. There is *always* a web server in the middle. You **never** connect directly to the real backend DB.

```
   CLIENT (front end)            MIDDLEWARE                    BACK END
 ┌──────────────────┐     ┌────────────────────────┐     ┌──────────────────┐
 │  Browser / App   │ ──▶ │  Web server            │ ──▶ │  Database        │
 │  (React UI)      │ req │   + CGI-bin / API layer│ SQL │  (Oracle, MySQL, │
 │  username+passwd │ ◀── │   (Perl/Python/Node/   │ ◀── │   SQL Server, …) │
 └──────────────────┘ resp│    Java servlet)       │data └──────────────────┘
       UNTRUSTED          └────────────────────────┘            TRUSTED
                                    │
                        (optional 4th tier inserted here)
                        Standalone middleware = Web Application Server / txn mgr
```

| Tier  | Name                                    | Job                                                          | Trust     |
| ----- | --------------------------------------- | ------------------------------------------------------------ | --------- |
| 1     | **Client / Front end**                  | UI, app, browser. Holds username+password only.              | Untrusted |
| 2     | **Middleware**                          | Web server **+** the script/API piece (CGI-bin, API) that connects to a DB. | —         |
| (2.5) | **Web Application Server** *(optional)* | Standalone middleware; transaction management; can generate HTML. | —         |
| 3     | **Back end**                            | The actual database. Almost **never** on the same machine as the web server. | Trusted   |

- **"Full stack"** = front end + back end. **Key correction:** the *web server was never the real backend* — the **database** is the backend.
- **Request → Response** in two steps. The whole world cannot log onto one database.
- Agents (Claude Code, "Hermes") can drive all of this 24/7 from your phone — but **the architecture is unchanged**.

**DoorDash example:** go to `doordash.com` → type "Indian food" → server runs `SELECT … WHERE item LIKE '%Indian%'` → formats results → you see restaurants. Pick one → another `SELECT` for that restaurant's dishes.

------

## 2. Static vs Dynamic HTML

|               | **Static HTML**                                          | **Dynamic HTML**                                    |
| ------------- | -------------------------------------------------------- | --------------------------------------------------- |
| Origin        | Tim Berners-Lee, HTML 1.0                                | Modern web                                          |
| Page          | Already built, sitting on disk (`.html`, `.jpg`, `.mp3`) | Built **on the fly** from a query                   |
| Example       | A fixed homepage                                         | Amazon search results page, assembled from many DBs |
| Server's role | Just **serve** the file                                  | Run a query → **format** results into HTML          |

A single Amazon product page is assembled from **many** databases: descriptions, images, pricing, star ratings, Q&A, recommendations. You see one tiny thing on your phone (**transparency** — you never see what's happening underneath).

------

## 3. History of Connectivity → Why Middleware Exists

- **Pre-web (before 1993):** No web server. **Dumb terminals** (ASCII/amber terminals) connected *directly* to a DB on a mainframe (e.g., IBM). **Trusted computing** — you knew exactly who every user was and handed out accounts one at a time. Front end → back end, simple, no public middleware.
- **1993:** World's first publicly available **web server**. This introduced the **three-piece architecture** (client / middleware / back end).
- Even on the old terminals there was a *form* of middleware: you sent **SQL through an API**.

------

## 4. The API Problem → SQL Became the Universal API ⭐ (exam)

Every DB vendor (Oracle, Microsoft SQL Server, etc.) stored tables in a **proprietary file format** and shipped its **own API**.

### The two-part API concept ⭐

Every API has **two halves**:

| Half                    | Faces                            | Published? | Who uses it                                     |
| ----------------------- | -------------------------------- | ---------- | ----------------------------------------------- |
| **Public** (high level) | The application programmer       | Yes        | Your code makes these calls                     |
| **Private** (low level) | The actual file format / storage | **Never**  | The vendor's driver translates public → private |

**The pain:** switch jobs/databases → learn an entirely new API. Endless re-learning for the *same* task (e.g., "write a report-generator over our DB").

**The fix:** **SQL became the standard public API.** Write **one** SQL program → runs on (almost) any DB. A **SQL driver** for each DB translates SQL → vendor-specific private calls.

> ⭐ **Exam:** *"What existed before SQL?"* → a **database-specific API** (each vendor different, no standardization). The lack of standardization is exactly what **led to** standardization (SQL).

> **Middleware = the API layer** between your program and the storage details. It **evolved into SQL**.

------

## 5. The Microsoft Data Stack — "Alphabet Soup" 🍜

The computing world splits into **Microsoft** vs **everyone else** (to counterbalance). Microsoft kept inventing proprietary formats, producing an "alphabet soup" of data APIs.

> **Marketing red flags:** Microsoft's words **"Open"** (ODBC) and **"Universal"** (UDA) are essentially **empty** — they mean *PC-only*. (Henry Ford analogy: *"any color, as long as it's black."*)

### 5a. The acronym table

| Acronym     | Full name                                  | What it is                                                   |
| ----------- | ------------------------------------------ | ------------------------------------------------------------ |
| **ODBC**    | **O**pen **D**ata**b**ase **C**onnectivity | Lowest-level PC DB driver API. **Exactly 2 levels** (public + private). **PC-only.** |
| **JDBC**    | **J**ava **D**ata**b**ase **C**onnectivity | Cross-platform DB API; shipped as a `.jar`. On a PC → bridges down to ODBC. |
| **OLE**     | **O**bject **L**inking & **E**mbedding     | Live-link/embed objects between two apps                     |
| **OLE DB**  | —                                          | The **DB flavor** of OLE                                     |
| **ADO**     | **A**ctive**X** **D**ata **O**bjects       | Higher-level data API over OLE DB                            |
| **ADO.NET** | —                                          | **Highest-level** MS data API; sits on top of everything     |
| **JET**     | **J**oint **E**ngine **T**echnology        | MS Access's DB engine. Rarely used alone (used via DAO). Later renamed **ACE** (Access … Engine). |
| **DAO**     | **D**ata **A**ccess **O**bjects            | API layer sitting **on top of JET**                          |
| **RDO**     | **R**emote **D**ata **O**bject             | Network/remote object access                                 |
| **UDA**     | **U**niversal **D**ata **A**ccess          | MS **umbrella** term for all of the above (still PC-only)    |
| **CLR**     | **C**ommon **L**anguage **R**untime        | .NET's virtual machine (Microsoft's "JVM")                   |
| **DLL**     | **D**ynamic **L**ink **L**ibrary           | Windows shared library (`.dll`)                              |

### 5b. ODBC details ⭐

- The **lowest-level** driver on a PC that a programmer can call.
- Lives in `C:\Windows\System32\` (e.g., `odbc32.dll`, `odbccp32.dll`) → these are **DLL** files.
- **Architecture = exactly TWO levels:** high-level **public** (what your program calls) ↔ **driver manager** ↔ low-level **private** (DB-specific binary read/write). Each DB has a different private driver; they all share one public ODBC API.
- **Never runs on Linux/Mac.** Access & Paradox are **PC-only** relational DBs.
- Delete the ODBC DLLs → you **break the Windows Database API** (nothing DB-related runs).

### 5c. DLLs & "Windows is a bag of services"

- **DLL = Dynamic Link Library.** *Dynamic linking* = the OS loads a library **on the fly** only when a program calls a function in it.
- **Why DLLs?** If everything compiled into one binary, Windows would be ~20 GB and **every tiny update** would force a full re-download. Splitting into DLLs → small, surgical updates.
- **Windows = component/service-oriented.** Task Manager → *Background processes* are these DLLs running as **services** (`services.msc` lists them all: audio, indexing, Windows Defender, etc.). The DB driver appears here once you run something that needs it.

### 5d. OLE / OLE DB — Object Linking & Embedding

Two apps (e.g., **PowerPoint + Excel**). Two ways to put an Excel chart into PowerPoint:

1. **Round trip (export/import):** Excel → save chart as PNG/PDF → import into PowerPoint. Static; you re-export on every change.
2. **Live embed (OLE):** the PowerPoint image is a **container fed live** by the spreadsheet. Edit the spreadsheet rows → the chart **auto-updates**. The link can be **bidirectional** (move a point on the chart → update the underlying row).

- **Maya + Photoshop example:** a Chinese symbol on Kung-Fu-Panda's shirt drawn in Photoshop is **live-linked** into the 3D model in Maya. Resize it in Photoshop → it changes in Maya instantly.
- **OLE DB** = same idea but the live source is an **actual database** (e.g., real-time e-commerce revenue feeding a live dashboard). **No export/import.**
- Implemented over the **COM** protocol (see §8).

### 5e. .NET / C# History — the Java Wars ⭐ (good story, testable context)

Around **1999–2000** Microsoft had a "come-to-Jesus moment": **Sun Microsystems** put **Java** everywhere ("**write once, run anywhere**"), making Windows look obsolete. Microsoft's attempts to **kill Java**:

1. **Visual J++** — their Java that ran **only on PC**. → **Sun sued, won**, MS had to stop selling it.
2. **Java libraries (DLLs)** that made Java code run only on PC. → **Sun sued again, won.**
3. **Radical fix:** hired **Anders Hejlsberg** (inventor of **Turbo Pascal**). Kept **Java syntax** but wrote their **own compiler** and **own VM** → renamed the language **C#**. Now Sun **couldn't sue** — you can't sue over how a language *looks*.

- **C# 1.0** ≈ a Java ripoff, but evolved into a strong language over time.
- **CLR (Common Language Runtime)** = the .NET VM (replaces the JVM). Can run bytecode compiled from C#, **VB.NET**, C++, etc.
- **".NET" = component-oriented architecture.** Windows + .NET + C# all name the **same family**.
- *(Meta moment in lecture: an AI assistant **hallucinated** when asked "did C# start as a Java ripoff?" — illustrating the hallucination point in §A.)*

### 5f. RDO — Remote Data Object (general object transport) ⭐

"**Remote**" = data fetched from **another machine** over a network is called an "object." Why it's a big deal — objects move across **wildly heterogeneous** machines:

- Machine A is **32-bit**, Machine B is **64-bit** (different integer sizes).
- **Little-endian vs big-endian** (byte order flipped → naïvely, your number becomes garbage).
- Different **OSes** (Linux, Solaris, IRIX), different **languages** (C++ vs C#).

…yet an object made on A can travel the wire and be **reconstructed** as a C# object on B, have its **methods run**, and be **sent back**. **Language, OS, endianness, datatype — none of it matters.** It's "just an object."

### 5g. ADO.NET workflow ⭐ (mirrors JDBC)

**ADO.NET = the highest-level MS data API.** Fully **backward compatible** (lowest level → … → ADO.NET on top). You can even **mix levels** (call JET, RDO, ADO, or ADO.NET) because high-level always compiles down to low-level.

1. **Connection** — connection string = **URL + username + password** → *Connection Manager*'s job.
2. **Command** — send a SQL query → *command executor*.
3. **DataSet** — result comes back as the **whole table in memory**. Survives even after you **disconnect**. Read **row by row** or **column by column**.
4. **Dump to XML** → then convert to **JSON**.

> Same architecture as **JDBC** (Connection class + Statement class). Neither ADO.NET nor JDBC is OLE.

**Legacy-data rescue trick:** write a modern **ADO.NET** program to read an old DB (**FoxPro, Paradox, dBase**), run `SELECT *`, pull the whole table, **dump as XML** → text representation → "save the day."

### 5h. ODBC architecture diagram (PC apps)

All PC apps (Paradox, FoxPro, dBase, Word, Excel, PowerPoint, even Flight Simulator) call **ODBC** one way or another. Stack (fully backward-compatible):

```
   ADO.NET  ─┐
   ADO       ─┤
   RDO       ─┼──▶  ODBC (public)  ──▶ driver manager ──▶ ODBC (private, DB-specific) ──▶ tables
   DAO       ─┤                          CREATE TABLE / INSERT INTO / CREATE INDEX
   JET       ─┘
```

------

## 6. DLL vs DSO — Windows vs Unix shared libraries ⭐

|                      | **Windows**                        | **Unix / Mac / Linux**              |
| -------------------- | ---------------------------------- | ----------------------------------- |
| Name                 | **DLL** = Dynamic **Link** Library | **DSO** = Dynamic **Shared** Object |
| Extension            | `.dll`                             | **`.so`**                           |
| Shared between apps? | Yes                                | Yes                                 |

- A `.c` file with a function → compile to `.o` → either **link into one executable**, *or* turn it into a **shared object** that many executables load at **runtime** → keeps every executable small.
- Find them on a Mac: `ls -lR /` and `grep` for `.so`.

------

## 7. JAR Files (and the famous interview question) ⭐

- **JDBC ships as a JAR.** Java's whole ecosystem is "**jar**" files (coffee-bean theme ☕).
- Each `.java` → compiles to a `.class`. **Many `.class` files** can be bundled into **one `.jar`**.

> ⭐ **Interview Q: "What makes a JAR runnable / why does double-clicking do nothing?"** A JAR holds **many classes**, and **each class can have its own `main()`** (Java allows multiple `main` methods — one per class). The **manifest must name the entry class** whose `main()` runs. If no `main` is designated (or no class has one), nothing happens. **You must bootstrap with one designated `main`.**

### JAR inspection tricks

- **See the classes:** rename `app.jar` → `app.zip` and open it — **every JAR is secretly a ZIP**.
- **Find `main`:** open a `.class` in a text editor (mostly binary junk) and search for `public static void main`.
- **`META-INF/MANIFEST.MF`** = the JAR's **"Amazon packing slip"** → lists the **`Main-Class:`**. If it points to a class **not inside** that JAR (e.g., `ij.ImageJ`), the JAR **won't run**.
- **Java packages = subdirectories.** `ij.ImageJ` = the `ImageJ` class inside the `ij/` folder.

**ImageJ example:** NIH / U.S. National Library of Medicine image-processing app, written in Java, packaged as a JAR. Run via double-click or `java -jar imagej.jar`. Effects: sharpen, erosion, color-negative, binary threshold (uses the **`BufferedImage`** class). Its `main()` lives in `ij.ImageJ`.

------

## 8. CORBA / OMG / IDL / COM / COM+ — cross-language object transport ⭐

|               | **CORBA**                                             | **COM / COM+**           |
| ------------- | ----------------------------------------------------- | ------------------------ |
| Defined by    | **OMG** (Object Management Group), 1980s Unix vendors | **Microsoft**            |
| Platform      | **Cross-platform**                                    | **Windows-only**         |
| Purpose       | Transport objects across languages/OSes seamlessly    | Same — but Windows-only  |
| Glue language | **IDL** (Interface Definition Language)               | COM IDL / type libraries |

- **OMG** = **O**bject **M**anagement **G**roup ("the **OG of ORB**" 😄). Met in the 1980s.
- **CORBA** = **C**ommon **O**bject **R**equest **B**roker **A**rchitecture. *Broker* = mediator. Middleware that lets different languages/platforms communicate.
- **IDL** (specified **1989**): at an abstract level **any object = a box of data (members) + code (methods).** IDL is a **minimal text representation** of an object. Serialize an object (any language) → IDL → send → reconstruct as a real in-memory object elsewhere → run a method → send back. (**Skeleton / stub** model.)

```idl
interface Hello {
    string sayHello();   // members + methods, minimally described
};
```

- **COM** = **C**omponent **O**bject **M**odel — Microsoft's Windows-only CORBA. A set of API calls that **serialize** objects (a.k.a. the **wire protocol**) for transport.
- **COM+** = "improved" COM, but it introduced **breaking, non-backward-compatible changes.**

> ⭐ **Software-engineering law:** **Changing an API is the biggest sin in development.** An API is a **sacred contract**. Break it (reorder pointers, add a param) and every dependent program breaks — forcing rewrites.

------

## 9. Aside — VHDL (the IDL analogy in hardware)

- **VHDL** = (V)HSIC **H**ardware **D**escription **L**anguage. Like IDL, it describes components at a **high level**; simple text → turns into **actual silicon**.

```vhdl
entity inverter is
    port ( a : in  std_logic;     -- "members" / signals
           y : out std_logic );
end inverter;
```

------

## 10. JDBC Core — the complete program ⭐⭐ (the heart of the exam)

> **Exam "three boxes":** ① **Connect** → ② **`executeQuery` (poke the SQL in HERE)** → ③ **Iterate**. The *magical* box is **②** where your SQL string actually goes to the DB.

### How JDBC can "log on" — `java.net.URL`

- Java's `java.net.URL` class lets a tiny program act like a browser: `import java.net.URL;` → `new URL("https://…")` → compile/run → you get whatever the server sends, in ~3 lines.
- **JDBC uses this internally** — the **connection string is a DB URL**.

### The full program

```java
import java.sql.*;

public class SelectExample {
    static final String URL   = "jdbc:mysql://localhost:3306/mydb";
    static final String USER  = "root";
    static final String PASS  = "password";
    static final String QUERY = "SELECT id, age, first, last FROM employees";

    public static void main(String[] args) {          // must have a main() to run
        try {
            // ① CONNECT  (DriverManager static method → Connection object)
            Connection conn = DriverManager.getConnection(URL, USER, PASS);

            // create a Statement object
            Statement stmt = conn.createStatement();

            // ② EXECUTE  ← this single line goes to the real DB via JDBC calls
            ResultSet rs = stmt.executeQuery(QUERY);    // returns a ResultSet (rows)

            // ③ ITERATE  (rs.next() = iterator: the "finger" sitting on the rows)
            while (rs.next()) {
                System.out.print(rs.getInt("id")     + " ");
                System.out.print(rs.getInt("age")    + " ");
                System.out.print(rs.getString("first")+ " ");
                System.out.println(rs.getString("last"));
            }
        } catch (Exception e) {
            e.printStackTrace();    // optional; drop try/catch and the code is even simpler
        }
    }
}
```

| Call                                         | Returns      | Note                                              |
| -------------------------------------------- | ------------ | ------------------------------------------------- |
| `DriverManager.getConnection(URL,user,pass)` | `Connection` | static method                                     |
| `conn.createStatement()`                     | `Statement`  |                                                   |
| `stmt.executeQuery(sql)`                     | `ResultSet`  | **the line that actually hits the DB**            |
| `rs.next()`                                  | `boolean`    | **iterator**; advances one row, `false` when done |
| `rs.getInt("col")` / `rs.getString("col")`   | value        | name the column + type → get the data             |

### Compile & run

```bash
javac SelectExample.java     # → SelectExample.class
java  SelectExample          # JVM runs main()
#   (use the CLASS NAME, not "java SelectExample.class")
```

### Iterator (`next()`) vs counted `for`-loop ⭐

- `rs.next()` is an **iterator method** — no `for (i=0; i<N; i++)` needed; you don't even need to know the row count.
- **Trade-off:** a **counted `for`-loop lets you SKIP rows** (e.g., `i += 10` to sample every 10th row); `next()` **insists on visiting every single row**. Same output if you just do `i++`.

### Bonus JDBC powers

`ResultSet` also supports `updateRow()`, `insertRow()`, etc. — you can push data **into** the table, not just read.

------

## 11. Recurring theme — Host language + Guest (SQL string) ⭐

For the **rest of the course**: a **host** programming language (Java / Python / JS) embeds a **guest** — a **SQL string** — sends it elsewhere (the DB), and gets results back (an array / result set you iterate). The host doesn't *understand* SQL; it just ships the string.

In production (e.g., a bank, World Bank data analyst): you still "just write SQL," but now the SQL runs server-side. Front end → server → (often via **MCP**) → real SQL on the backend → server formats HTML → you see a clean table. **You never see raw data** — the server formats it.

------

## 12. The Web Tier — Full Stack, CDN, E-commerce

- **WWW changed everything:** everyone became both **producer** and **consumer** of data. *Every* click, upload, retweet, like/unlike, add-to-cart (even without buying), and return is **stored**.
- **Full stack:** untrusted **React** front end (+ username/password) → **web server** → **database**. **Never** log directly into the backend DB.
- **CDN (Content Delivery Network):** the Amazon catalog is **replicated worldwide**. A **reverse proxy** machine *looks like* `amazon.com` but **routes you to the nearest copy** (Japan, Canada, India, UK). More complex than one-machine/one-DB, conceptually identical.
- **E-commerce** (Amazon) drove the whole explosion.

------

## 13. Server-Side Extension & CGI ⭐

- The web server's **core job** = serve **static** files (HTML, JPEG, PDF, MP3).
- The **extra part** = a **server-side extension** that runs **scripts** (Perl, Python/Flask/Bottle, Node.js). Those scripts hold **connection calls (like JDBC)** to log onto a DB and run SQL. **The DB has no idea who's calling** — that's the beauty.
- **Apache:** filesystem root `/` → make a **`/cgi-bin`** directory → drop programs in it. A request **kicks off** a program, passes it input, the program hits the DB.
  - **CGI** = **C**ommon **G**ateway **I**nterface. Dir is literally `cgi-bin` (lowercase; configurable).
- **Netscape 1.0 era — external forms:** subscribe to a magazine → fill a form → **POST** (sending data to a server) → server hands form data to a **Perl** program → it stores you in the DB → returns "succeeded."

### CGI-bin vs API

- **CGI-bin** = loosely structured (a **scripting** language).
- **API** = the *same thing*, more **structured** (e.g., a **Java API** using JDBC).
- **Servlet vs Applet:** Java on the **server** = a **servlet**; Java on the **client** = an **applet** (browsers blocked client-side Java for security). Java got **relegated to the server**, where being a **secure** language is a "match made in heaven."

------

## 14. Dynamic HTML Generation & Server-Side Rendering (SSR) ⭐

- **CGI program → API calls → DB → raw/column data → format into HTML** = **dynamic HTML generation**.
  - *Example (Blick Art Materials):* search "watercolor" → query → a product **table formatted by the server** (no pre-existing page). Add `WHERE` conditions (manufacturer = "Daniel Smith", in-cart, …) → fewer rows pass through.
- **Server-Side Rendering (SSR):** the server can render **React** code (not just raw HTML) and send **pre-rendered React** to the client. The **component hierarchy** (nested components = a tree) is built **on the server**; the client receives a JavaScript **dependency graph** and just displays it. **The server renders, not the browser.**
- Whatever you see in an app = a **component hierarchy** turned into UI (buttons = how you interact).

------

## 15. Perl CGI / DBI — the original ⭐

- **Perl came first** (CGI). **Java (JDBC)** and **Microsoft (ODBC)** *borrowed* the idea from Perl.
- In Perl every library = a **module**; **DBI** = the **first DB-connection module** ever written. Perl uses **`$`** for scalar variables.

```perl
use DBI;

my $dbh = DBI->connect($dsn, $user, $pass);                  # connection handle (object)
my $sth = $dbh->prepare("SELECT patient, start, name FROM visits");  # statement handle
$sth->execute();                                             # actually runs on the DB
while (my @row = $sth->fetchrow_array()) {                   # iterator → fills @row
    print "@row\n";                                          # like Python: for i in list
}
```

Run: `perl report.pl` → prints **raw text** from the DB in a bash/Unix shell.

### Same code, but emit HTML (this *is* SSR, since 1993)

```perl
print "Content-type: text/html\n\n";                 # header
print "<table>";
while (my @row = $sth->fetchrow_array()) {
    print "<tr><td>$row[0]</td><td>$row[1]</td></tr>";   # server builds the HTML
}
print "</table>";
```

Perl sends **data + formatting**; the client just **renders** it.

### Larry Wall (Perl's inventor) — the 3 Virtues of a Great Programmer ⭐ (fun/likely-quoted)

1. **Laziness** — don't type too much (hence `i++` over `i = i + 1`).
2. **Impatience.**
3. **Hubris** — excessive pride in your work.

- **Obfuscated Perl Contest:** Perl has *too many* operators → you can write code that's nearly unreadable but still works (e.g., **Minesweeper** in a few lines). Powerful, but **dangerous** — sloppy Perl can crash/take over a server.

------

## 16. Java's many client/server mechanisms — "1995 already had Agents" ⭐

From day one, Java shipped multiple networking mechanisms:

| Mechanism                          | What it does                                                 |
| ---------------------------------- | ------------------------------------------------------------ |
| **Applets**                        | Java in the browser (**no longer works**)                    |
| **Socket class**                   | **UDP** (streaming, no ACK) and **TCP/IP**                   |
| **Servlets**                       | Java running **on the server** (server-side counterpart of applets) |
| **RMI** (Remote Method Invocation) | With permission, **log onto another machine by IP and run code there** — even directly on the backend DB from your front end |
| **CORBA support**                  | Object serialization across languages/OSes                   |

> **"Nothing is new":** In **1995** you could start a Java program, **log off, and it kept running** — exactly like a 2026 agent ("Hermes") that completes a task while you sleep.

------

## 17. Web Services History — SOAP / WSDL / UDDI ⭐ (the triangle)

~20 years ago: bulky PC front end still wanting **services** from a backend.

| Piece    | Full name                                                    | Role                                                     |
| -------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| **SOAP** | **S**imple **O**bject **A**ccess **P**rotocol                | **XML** message format for request/response              |
| **WSDL** | **W**eb **S**ervices **D**escription **L**anguage            | **Describes** the service / its operations               |
| **UDDI** | **U**niversal **D**escription, **D**iscovery & **I**ntegration | **Registry / "yellow pages"** to publish & find services |

- Everything was **XML** back-and-forth. Client builds an XML SOAP doc → server → looks up service → returns XML.
- **Rule:** unless you **advertise** your service in the **registry (UDDI)**, **nobody can find it.**
- **Modern parallel:** agents can do ~20,000 things → you now need **agent registries** — *the same idea from the early '90s.* **Nothing in Agents is truly new.**

------

## 18. REST API ⭐⭐ (the core modern topic)

A client makes a request to a server **as a URL with query parameters** — i.e., **calling a function over a URL**.

```
GET https://api.example.com/stock?symbol=AAPL&period=2024&high=yes
         └──── endpoint (URL) ────┘     └──── key=value args, joined by & ────┘
```

- **Before `?`** = the URL/endpoint. **After `?`** = `key=value` pairs (the **function arguments**) joined by `&`.
- Trivial example: `…/add?a=2&b=4`.
- The server can do **anything** with a REST call: run locally, hit a DB (SQL), or call a **microservice**.
- **Hundreds of thousands** of REST APIs exist. Even **Google search** is REST: `google.com/search?q=la+weather` (**`q`** = key, your search = value).

### Other communication protocols (for context)

| Protocol      | Notes                                                        |
| ------------- | ------------------------------------------------------------ |
| **WebSocket** | Mostly JavaScript; React front/back                          |
| **gRPC**      | Google; **high-bandwidth** client-server (e.g., transferring lots of data / media) |
| **REST**      | URL + query params *(focus)*                                 |
| **GraphQL**   | Wraps REST *(focus)*                                         |

------

## 19. GraphQL & MCP — the modern API stack ⭐

```
   ┌─────────────┐  ← agent asks "what can you do?", sends plain-text requests
   │     MCP     │     (top)
   ├─────────────┤
   │   GraphQL   │     (middle) — wraps REST; client GraphQL request → REST request
   ├─────────────┤
   │    REST     │     (bottom) — URL + query params
   └─────────────┘
```

- **MCP flow:** the agent asks the **MCP server** what it can do → the server **describes functions + parameters in plain English** (e.g., stock lookup: send a symbol, *optionally* a time range, *optionally* a "highest value" flag). The agent sends a **plain-text** request → MCP **matches it to the real API call** → calls it → returns **text** to the front end.
- **Critical point:** several layers deep, **the underlying REST calls never change.** MCP just bolts **plain text on top** = "Agent Magic."

------

## 20. Web Application Server (the optional 4th tier) & ColdFusion ⭐

- Insert one more machine between web server and DB = **standalone middleware** = **Web Application Server (WAS)**. "Application" mostly means **database**. It **offloads** work and can **generate HTML**, so the web server purely serves HTML.
- Examples: **Tomcat** (Apache, **Java** servlet container — *lecture guessed "Python," but it's Java*), **WebSphere** (IBM; mainframe shops favor it). All expose an **API**; a WAS can run **ColdFusion**.

### ColdFusion / CFML — templates ("fill in the blanks")

- **CFML** = ColdFusion Markup Language. *Looks like* HTML but **isn't** — it's a **template**. The WAS knows to hit the DB, fetch data, **fill the template** → emit **real HTML** → the client renders it (oblivious to what happened).

```cfml
<cfquery name="getBooks" datasource="library">
    SELECT title, author, year FROM books     <!-- run SQL / stored procedure -->
</cfquery>

<table>
<cfoutput query="getBooks">
    <tr><td>#title#</td><td>#author#</td><td>#year#</td></tr>   <!-- placeholders get hydrated -->
</cfoutput>
</table>
```

- **Template (no data) + query result (data) → "hydrated" → real HTML table.** Pure **server-side templating / replacement.**

------

## 21. Microservices + Containers + Cloud + Kubernetes ⭐ (the modern powerful architecture)

The front end becomes a **conductor** orchestrating **many** backends — each a tiny **service**:

- DB access, **search engines** (Google, DuckDuckGo, **Elasticsearch / Lucene**), **compute** (e.g., a million digits of π), **weather**, **stock prices**, **credit-card processing**, **sensor/camera** lookups, …

```
                 ┌──▶ [microservice: DB]        (container)
   FRONT END ────┼──▶ [microservice: search]    (container)   ┐ AWS / GCP cloud
  (conductor)    ┼──▶ [microservice: weather]   (container)   │ orchestrated by
                 ┼──▶ [microservice: payments]  (container)   ┘ KUBERNETES
                 └──▶ [microservice: sensors]   (container)
```

- **Microservice** = one service does **one thing**; all are separated. The app = the **combination** of many.
- Microservices run on the cloud (**AWS, GCP**) **inside containers** (the cloud doesn't run the service directly).
- **Kubernetes** = container **cluster manager**: knows how many containers exist, **spins up more** under load (nobody waits), **deletes** them when demand drops = **elastic cloud computing**.
- **Microservices + Containers + Cloud = radically powerful** — the front end just gets its data; the backends can be in **any number of languages** and it doesn't matter.

------

## 22. Quick-Reference: Exam Pointers 🎯

- **3-tier:** client (untrusted) / middleware (web server + CGI/API) / database (trusted, separate machine). 4th tier = Web App Server.
- **Before SQL:** database-specific APIs (no standardization) → that pain **created** SQL as the universal API.
- **Every API has 2 halves:** public (programmer-facing) + private (never published). SQL drivers translate public → private.
- **ODBC = exactly 2 levels**, PC-only, lives in `System32` as `.dll`. **JDBC** = cross-platform, ships as `.jar`; on a PC it **bridges to ODBC**.
- **DLL (`.dll`, Windows) ↔ DSO (`.so`, Unix).**
- **JAR runnability:** manifest's `Main-Class` must name a class with `main()` inside the JAR; rename `.jar`→`.zip` to inspect.
- **JDBC three boxes:** `getConnection` → **`executeQuery(sql)`** → `while(rs.next())`. `next()` = iterator; a `for`-loop's advantage is **skipping rows**.
- **CORBA (cross-platform, OMG) vs COM/COM+ (Windows, Microsoft)**; glue = **IDL**. Changing an API = cardinal sin.
- **Web services triangle:** SOAP (XML msg) + WSDL (describe) + UDDI (registry).
- **Modern stack:** REST (URL + `?key=value&…`) → GraphQL → MCP. Underlying REST never changes.
- **Perl/DBI** first; **Larry Wall's virtues:** laziness, impatience, hubris.
- **Microservices + containers + Kubernetes + cloud** = elastic, language-agnostic backends.

------

## Appendix A — Non-curricular asides (mentioned in lecture)

*Captured for completeness; not core exam material. Product claims below are the **lecturer's**, stated as-is.*

- **AI job-application tool (Fernando, open-source):** takes your résumé → finds jobs you qualify for → **tailors** the résumé per job (rearranges, doesn't lie) → writes a cover letter. Targeted, not spray-and-pray.
- **Claude Code as a frontend for any backend:** point the `ANTHROPIC_*` base-URL env var at a **local LLM** (e.g., Llama/Gemma on localhost) → use the agentic loop at zero token cost; swap backends to compare code quality.
- **"Fable" / "Mythos" (lecturer's claim):** a very large (~10T-param) model said to be released; *Fable* = general-purpose, *Mythos* = cybersecurity-focused; *Fable* reportedly free initially then expensive — "don't get dependent." *(Treat specifics as unverified lecture-hall commentary.)*
- **Google "AI Overview" lawsuit (German firms, ~June 11):** a court reportedly held **Google responsible** for AI-generated summary text (defamation), rejecting the "users can click the links" defense — *"you can't call it a summary and disclaim its words."* Flagged as a landmark for AI-hallucination liability (medical/financial/legal stakes).
- **Why LLMs always hallucinate (architecture point):** a similarity/vector measure will **always find \*something\*** related to a prompt, even far outside the model's "wheelhouse," and answer **confidently** — the model **doesn't know where its knowledge boundary is** or when to say "ask an expert."
- **HW2 preview (two LLMs):** LLM #1 generates **SQL** from a text description; LLM #2 (on **TiDB Cloud**) **auto-populates sample data** and you **verify** the SQL returns the right answer. ~a couple of days.



# 6/16 Lecture: Database Systems — Performance Tuning, Indexing & Connectivity (Cheatsheet)

> Lecture covered: (1) wrap-up of the **connectivity** unit (REST / GraphQL / MCP), (2) the start of **performance tuning** — caching + the optimizer, and (3) **indexing** + a few **good-SQL** rules. Ends teasing **data warehousing / BI / data mining** for next time. The optimizer-hints + "no math on indexed columns" topic is **to be continued tomorrow**.

------

## 0. Lecture opener (context / tangents — *not* core exam material)

- **Anthropic export-control ban**: An **ECD (Export Control Directive)** from the Commerce Dept led Anthropic to suspend access to its top-tier models **Mythos** and **Fable** (Fable = the more open variant; same underlying capability). Trigger: a security researcher used Fable to find a routine site vulnerability; the chain of events (Amazon/White House) escalated it. Many cybersecurity researchers signed an open letter (`freefable.org`) arguing it was overreach. Analogy drawn: **Phil Zimmermann's PGP (1991/96)** — gov't treated strong public-key crypto (RSA, asymmetric keys) like a weapon.
- **China models**: open-weight models (e.g. **GLM / Zhipu**, **Kimi K2.7** — note your HW used **K2.6**) are only "a few months behind"; argument that bans don't help.
- **Free local stack idea**: run **Claude Code** but point the API base URL (env var) at **localhost** (Ollama running Llama / Gemma / GLM / Kimi). "Intelligence is in the harness/loop, not the LLM — swap the model freely." Also mentioned: **Kiro** (Amazon's free agentic IDE), **Hermes** (chat-driven agent control).

### Evolution of "X engineering" (conceptual timeline)

**Prompt engineering** → **RAG** (retrieval-augmented generation; external DB of PDFs/sheets/images feeds the LLM) → **Context engineering** → **Prompt chaining / Agents** (break a prompt into chained function calls) → **Tree of Thought** → **Graph of Thought** → **Agents** → **Harness/memory engineering** → **Loop engineering**.

- **Agent = an (effectively) infinite loop** that **ReAct**s: *reason → act (run tools) → reason → act …* until the **goal is met**, then returns. No babysitting.
- Best practice: **separate generator and critic** — the agent that writes code should *not* be the one that certifies its tests. Use a different agent/developer to verify.
- Agents **cache what works** ("compile" successful steps into a skills file) → incrementally self-improve. Pioneered/popularized as the **"Karpathy loop."**

------

## 1. Connectivity wrap-up

### Full stack = 3 layers (optionally 4)

```
[ Front end ]  →  [ Web server (middleware) ]  →  [ Back end / Database ]
 phone/tablet/      Flask, Bottle, Node.js,        SQL store
 laptop, React      Express, Axios, ...            (rarely changes)

(optional 4th) [ Web Application Server ] between web server & DB
   → offloads HTML generation OR transaction management (partition the labor)
```

The front end turns clicks/filters into a request → server translates it into **SQL** → DB returns **result set** → server/client renders it (React component, etc.). *Back-end DB world hardly changes; only the delivery mechanism keeps evolving.*

### REST API

- Many small **function-like calls** ("search commands"). One site can expose dozens (e.g. a stock API: one call = "give me symbol," another = "symbol + timeframe," etc.).
- **GET request** → lightweight, **everything appended to the URL**: `…/path?key1=value1&key2=value2` (the `?` splits URL from the `key=value` pairs).
- **POST request** → **dump actual data** to the server (upload a résumé, send a file/music). Used when payload is too big for a URL.
- Response is almost always **JSON** (the UI makes it pretty; raw JSON is boring `{…}`).
- REST is **low-level / "too detailed"**: you must ask very specifically, and it often **returns too much** → you filter client-side.

### GraphQL

- **A wrapper layer over REST — not a replacement.** 100% backward compatible; a GraphQL query typically ends up calling existing REST calls underneath.
- Sent via **POST** (browser → server directly; safer + more efficient).
- Looks like **"partial JSON" — keys only, no colons/values**: you send the *shape* of what you want; the server fills only those fields.
- **Aggregates multiple REST calls** and **filters** the result: ask for 3 fields out of 100 (or 4 of 40 across 4 calls) and get back exactly those 3. Saves you from manual multi-call + merge + trim.

### MCP (Model Context Protocol) — the **plain-English** layer

- Think **"USB port"**: once something speaks MCP, you can plug an agent into it.
- Wraps an API (REST/GraphQL) so you query in **natural language**; the **MCP server** translates NL → the right API call, runs it, and returns **JSON** → the LLM answers you.
- **Discovery phase** (catch-22 fix): client first asks "what can you do?" → server lists capabilities → client picks one → server says what params it needs → client sends them → server returns results. **All JSON.**
- **Everything is JSON-based**; you make your own MCP server. Thousands exist (GitHub repo lists them: GitHub, Google Drive/Maps, Gmail, file system, Slack, Puppeteer (drive a browser), Photoshop/Firefly, Maya/Blender, etc.). Anthropic launched MCP in **late 2024**; took over fast.

### Other protocols (lighter coverage)

| Protocol      | What it is                                                   |
| ------------- | ------------------------------------------------------------ |
| **Webhook**   | Front-end JS calls a server-side JS function directly; result returns to you. |
| **gRPC**      | Google protocol using **protocol buffers** (hierarchical, efficient binary format) for client↔server transfer. Great when the server sends a lot. |
| **WebSocket** | JS-only, browser↔browser live channel (e.g. jam live: you hear my guitar, I hear your drums). |
| **SOAP**      | Oldest "web service" form. Send request → get response.      |
| **MQTT**      | **IoT sensor connectivity** (tire pressure chip, room temp, rainfall) → device sends data to an app. |

- **Server-Side Rendering (SSR)**: server builds fully-populated HTML / React components and ships them; the client just displays. (Opposite of "send JSON, let client render.")
- **CGI-bin vs API call**: both just mechanisms that ultimately translate a query into something the DB runs.
- Cloud (**AWS ~53 services**, Azure, GCP) can host REST/GraphQL globally, plus storage, compute, ML hosting (**Bedrock** = deploy your LLM/app as a service). All learnable **free locally first**, then deploy.

### Live example — The Movie DB REST call

```
https://api.themoviedb.org/3/search/multi?api_key=YOUR_KEY&language=en-US&query=game
```

- Structure: base URL `/3/search/multi`, then `?`, then `key=value` pairs (`api_key`, `language`, `query`).
- **`api_key`** is the standard contract key (identifies/bills you; yours ≠ mine).
- Like a function call: `search(api_key=…, language="en-US", query="game")`.
- Returns **JSON** (movie objects: name, poster image path, etc.). Client then requests the JPEG by filename → renders the poster grid. **Server's job = raw JSON; client's job = the pretty UI.** (Also a **Dog CEO API** demo: `breeds/list/all`, random dog image.)

------

## 2. Performance Tuning — overview

**Setup:** two DBs, same data/tables/rows; same query → one returns instantly, the other spins for seconds with the *same* result. Everyone prefers the fast one. **Tune = make it as fast as possible (one word: SPEED).** Analogy: a **tuned race car** + a **pit crew** swapping a tire in 10s.

### Where you tune

- **Server side** = the database itself (DBA's job; usually done for you in the cloud).
- **Client side** = **better SQL** (more interesting / what *you* control).
- Usually do **both**.

### "Weak link in a chain" — fix ALL or none

Make **RAM, CPU, disk, and network bandwidth** all optimal. (Cheap CPU = slow queries; too little RAM = swap/disk thrash; old slow disk; slow network — any one bottlenecks everything. "Why lock a vault all week then leave it open on the weekend?")

------

## 3. DBMS internals — what matters vs. what doesn't

Mental model — **work on a LOCAL COPY; touch the real DB rarely:**

```
   [ Client / App ]                       [ REAL Database ]
   (you, tapping "buy")                   (permanent, ACID-durable)
        |                                       ^
        | read / query                          | COMMIT  ← thin, FRAGILE wire.
        v          run SQL locally              |          Use as little as possible!
   [ Data Cache ] ── insert / update / ─────────+
   (local copy)      delete / create / drop
```

- All edits happen in the **local copy** (e.g. an **Amazon shopping cart**). Nothing permanent changes until **COMMIT** (= "Buy" / 1-click). After commit, **undo can't reverse it** — it's etched in (ACID **Durability**).

**Components (and which ones DON'T affect tuning):**

| Component              | Role                                                         | Tuning-relevant?   |
| ---------------------- | ------------------------------------------------------------ | ------------------ |
| **User process / IAM** | Identity → **Authentication** ("are you who you say?") + **Authorization** ("are you allowed to see this?"). | ❌                  |
| **Log manager**        | Transaction management (locks/logs).                         | ❌                  |
| **Scheduler**          | Like log manager — transaction management.                   | ❌                  |
| **Listener / parser**  | Syntax check ("valid SQL? missing semicolon?"). Kicks out bad SQL. *Now matters more because AI writes broken SQL.* | ❌ (not optimizing) |
| **Optimizer**          | **Generates the ACCESS PLAN.** The real work.                | ✅                  |

➡️ **All of performance tuning reduces to THREE things: `SQL Cache` · `Data Cache` · `Optimizer`.**

------

## 4. SQL Cache (most important cache)

- **SQL you write ≠ what actually runs** — just like C++ must be **compiled** for a specific machine. Compiling SQL = **optimization**; the output is an **ACCESS PLAN** (the most efficient way to read the rows/columns and write results back).
- **Same query run repeatedly** (e.g. an advisor pulling the same transcript): why recompile? → **Cache it.**
- Cache stores **(query → access plan)** as a **key–value pair**. Next run: look up first; **hit → reuse the plan**, **miss → optimize once, then store** for next time. Cache grows with usage.
- **Eviction** when full: drop **oldest** (store a **timestamp**) or **least-reused** (store a **use count**) entries.

### Hashing the query (so the key is small)

Real SQL queries can be pages long — storing raw text wastes space. So **digest the query with a hash function** and store the **hash → access plan**.

- **Hash functions:** `MD5` (128-bit, **mathematically BROKEN** — fine for SQL keys, not for security) · `SHA-256` (256-bit, **secure**) · `SHA-512` (512-bit, **max strength / future-proof**).
- **Properties:**
  1. **Deterministic** — same input always → same fixed-length output (works for "MD5 is cold!" up to a 10-TB textbook).
  2. **Avalanche** — change *one* comma → the whole digest changes radically (no small-change/small-change).
  3. **One-way / irreversible** — cannot recover the input from the hash.
- Therefore: **hash the SQL (key)**, but **NEVER hash the access plan (value)** — you can `gzip`/`tar` (compress) the plan, but a hash can't be reversed back into a plan.
- Store digests **sorted** → **binary search** to check a hit instantly. (Also called **signature / digest / hash**.)

> *Tangent:* NSA's **Codebreaker Challenge** (annual, ~Sep) — malware RE, crypto, network forensics, vuln research.

------

## 5. Data Cache (a.k.a. Buffer Cache)

- **Simply a local copy of data** pulled from the real DB. Your SQL **runs on the copy**; when finalized, **COMMIT echoes changes to the permanent copy**. Result sets return to the user; only commit travels back to the real DB.
- **ACID = Atomicity, Consistency, Isolation, Durability** (Durability = permanent after commit).
- Storage terms:
  - **Data file** — where all files live ("binary file format").
  - **Extent** — the increment the OS grants when a table fills (e.g. **+50 MB** each time). Too small → constant re-requests; too large → wasted/unused space. **Find a good extent by trial & error** (depends on fill rate).
  - **File group / Table space** — a collection of tables = a database (one virtual namespace accessed together).
- ⚠️ **Access plans are NOT portable** (unlike SQL, which is portable like C++). A plan depends on the engine's binary file format → **Oracle's plan ≠ MySQL's plan**. Same high-level job, totally different bottom-level implementation.

------

## 6. The Optimizer — query optimization

The optimizer **analyzes the SQL and generates the access plan** (the efficient way to access data). It's tuned along **three independent dimensions** — pick a combination, watch the stats, adjust, repeat (an LLM can suggest good combos by reading access patterns):

### Dimension 1 — Operation mode: **Manual vs Automatic**

- **Automatic** (default, convenient) — the DBMS/DBA decides; no intervention. *(Like an automatic car / phone camera in auto.)*
- **Manual** — for "control freaks" who know access plans better than the system. *(Manual transmission / manual aperture & light-meter.)*

### Dimension 2 — Timing: **Static vs Dynamic**

- **Static** — build **one** access plan and **run it blindly**, ignoring any mid-run changes (RAM running out, tables added). Cheap to produce; good for **embedded queries** (same button → same query). *(Analogy: paper **Thomas Guide** map — no live updates; **compile-time** error / **static** memory allocation `int a[10000000]`.)*
- **Dynamic** — can **modify the rest of the plan at runtime** as conditions change. More work to produce, but the query usually runs faster. *(Analogy: **Waze** rerouting live while you drive — "God watching from above"; **runtime** error / **dynamic** allocation `malloc`/`new` on the heap.)*

### Dimension 3 — Type of information: **Statistics (cost-based) vs Rules**

- **Statistics / cost-based** — data the DBMS auto-collects about how queries/tables behave (≈ **data-driven AI = Machine Learning**). "This query looks like a past one → use that plan."
- **Rule-based** — **human/DBA-written rules** ("always access table A before B," "fetch ≤100 rows") (≈ **symbolic / Good-Old-Fashioned AI (GOFAI)**, **expert systems**).
- **This is the same split as the 3 branches of AI** (🚩 *exam-style "weird question"*):
  - **Statistics ↔ Machine Learning** (supervised = labeled data; unsupervised = raw/unlabeled — both **data-driven**).
  - **Rules ↔ Symbolic AI** (logic/symbol processing, expert systems).
  - **3rd branch = Reinforcement Learning** (give a goal, not the actions; reward/punish on goal-met). *Possible on a DB but rarely used.* (Knowledge graphs are still symbolic.)

> **Expert system** = **Knowledge Base** (rules captured from human experts) + **Inference Engine** (does logical chaining over the rules) → answers questions. *The knowledge comes from a human, not from data.* **Cyc project** (the prof worked on it): goal = encode **~30M pieces of common sense** (interview ordinary people) into rules; the world was carved into rigid categories (tangible/intangible objects, spatial things, time intervals, etc.). Result: more rules did **not** create intelligence → contributed to an **AI winter**. ~10 yrs, ~$30M.

**Statistics you can measure (inputs to cost-based optimization):** # rows, # disk blocks / table size, row length (# & types of columns), **# distinct values per column**, block/extent size, data-file location, and most importantly **indexes**. Collect manually (Oracle: `compute statistics`) or automatically (e.g. a **cron job** every N minutes).

### Sub-splits (it's a tree)

`Statistics → {Manual, Dynamic, …}` etc. — i.e. the three dimensions combine. The slide labeled **"rule vs cost"** is the same thing: **rule** = human rules, **cost** = statistics.

------

## 7. Query processing steps

```
SQL text → [ PARSE ]  syntax/validity check (mechanical; matters now due to AI-written bad SQL)
         → [ OPTIMIZE ]  build ACCESS PLAN  (check SQL Cache: HIT → reuse;  MISS → optimize then store)
         → [ EXECUTE ]  do I/O: retrieve data blocks into the Data Cache, run the plan LOCALLY
         → [ FETCH ]    return result rows to the user
```

- **Parse** = "is this valid SQL?" (proprietary internals differ per vendor; SQL → "exe/plan" like C++ → `.exe`).
- **Optimize** = the heart; produces the (non-portable) access plan; cache it if absent. One-time work — runs 2nd/3rd/… time reuse it.
- **Execute (I/O)** = the part that actually hits the DB and pulls data blocks; the access plan runs **locally** on the cached copy; transactions/locks apply (same row being computed → lock it).
- **Fetch** = better called **"return"**: send rows back to the user. ⚠️ **Cursor/pagination gotcha** — don't ship the whole buffer at once; a small protocol sends **more only when the client scrolls** ("scroll for more").

> Browser analogy: when updated homework "looks missing," your browser shows the **local cache** → **Shift-Reload** forces a real fetch. Same caching idea.

------

## 8. Indexing ⭐ (the #1 practical lever)

**An INDEX is a new table** (costs disk space) whose **only job is query optimization**. Delete it → optimization gone, back to full scan. Build it by **sorting a column** (the rest of each row rides along) → enables **binary search** instead of a **raw table scan**.

### Why it's huge (complexity)

| Search                              | Cost         | Note                                                   |
| ----------------------------------- | ------------ | ------------------------------------------------------ |
| **Raw table scan** (unsorted)       | **O(n)**     | Worst case checks all n rows. Avoid "like the plague." |
| **Binary search** (sorted / B-tree) | **O(log n)** | Throw away half each step.                             |
| **Hash**                            | **O(1)**     | No search — function points straight to the row.       |

- **log₂(1,000,000,000) ≈ 30** (since `2³⁰ ≈ 1.07B`). So **~30 comparisons vs 1 billion** → "like 1 second vs 1+ day."
- **Range search** (e.g. GPA between 2.95 and 3.0, salary 100K–200K, stocks $100–$200): do **two binary searches** (find top, find bottom) and **blindly return everything in between** — guaranteed correct because it's sorted.
- **State-recall example** (car-seat recall, must notify customers in 24h): with ~50 US states, pretend 64 = `2⁶` → find any state in **≤6 jumps** vs scanning 50 (Amazon: ~400M people). ~8× faster.
- **Birthday example**: index DOB (365 values) → at midnight, **intersect** "people born today" with your friends list → wish them happy birthday. Same intersection trick social apps use.

### Book-index analogy

The alphabetical **index at the back of a book** maps keyword → page numbers. Because it's **sorted**, you flip back and forth (binary-ish) to find "table" fast. Unsorted index = useless. *Indexers are a real (mildly technical) job.* **Sorting is the magic.**

### Sparsity (cardinality) — what to index

**Sparsity = number of distinct values in a column.**

- **Low sparsity → DON'T index** (e.g. **gender** = 2–3 values: each index entry maps to a huge pile of rows → no benefit).
- **High sparsity → DO index** (state = 50, **GPA ≈ 401** at 2 decimals, **DOB = 365/366**, IDs, prices, names).

### Index data structures

| Structure                                  | Cost      | How                                                          |
| ------------------------------------------ | --------- | ------------------------------------------------------------ |
| **B-tree** (binary search tree / **heap**) | O(log n)  | At each node compare (< → left, > → right), discard half. Leaf nodes hold **row IDs** (small collisions OK). |
| **Hash index**                             | **O(1)**  | `value → hash(value) → slot # → row_id → real row`. No sorting/search at all. **Collisions** (2 values → same slot) → tiny local search; minimize them. |
| **Bitmap index**                           | very fast | For **low-cardinality categories** (e.g. 8 compass directions). One column per category; set exactly **one bit = 1** per row (**one-hot**). Query with a **hardware mask + AND** (e.g. mask `010`, AND each row → keep the 1s). |

**B-tree details:** it's a **heap tree** — for any node, the right subtree > node > left subtree; any new value (even "Z") routes deterministically. As inserts pile up the tree can get lopsided → **rebalance / rotate** (analogy: **wheel alignment** so the car doesn't pull left/right).

**Hash collisions:** good hash fn spreads values out (few collisions). If a slot has 2+ row IDs, do a small search within it. Books example: `Great Gatsby`, `Grapes of Wrath`… each hashes to a slot holding its row ID.

### One-hot encoding (🚩 exam "name this")

A row turns on **exactly one bit = 1**, all others **0** (analogy: only the **live wire** shocks you; only one switch on). Encodes categories (colors, grade letters A/B/C, compass directions) for fast bitmap search and for ML.

- **One-hot** (correct): `A → 100`, `B → 010`, `C → 001` (one 1 only).
- **Binary encoding** (NOT one-hot): e.g. `green → 011` packs multiple 1s — more compact but *not* one-hot. **Don't confuse them.**

### Cuckoo hashing (tangent → real system)

```
Table1[hash1]   Table2[hash2]
B → wants slot occupied by A → EVICT A → A rehashed into Table2
A → occupied by C → EVICT C → C rehashed → ... → all placed after a few "bounces"
```

- Like a **cuckoo bird** kicking another out of the nest. Often **faster than handling collisions**; if no empty slot exists anywhere, you fall back to living with a collision.
- **Open question / thesis bait:** why stop at 2 tables? Try **N** tables — does it keep getting faster, or is there a bounce limit?
- Real use: **TikTok "Monolith"** real-time recommendation engine — **near-collision-less embedding** (paper on arXiv). The hashing is one piece of the larger engine.

### Index selectivity

Creating an index **does not force** the optimizer to use it — that decision is **selectivity**. Make **highly selectable** indexes (high-cardinality columns); low-sparsity ones get ignored.

### Where indexes pay off (candidate columns)

- **`WHERE` clause** columns (find the column in the condition → index it).
- **`GROUP BY`**, **`ORDER BY`**, **`JOIN` condition** columns.
- **MIN/MAX queries** (just read top/bottom of the sorted index — no scan).
- **Computed columns** are fine to index too (e.g. `base_salary + commission`).
- One table → **many indexes** (each on a different column); drop any when done. **Never reorganize the main (raw) table** — that's the **raw table scan** you're avoiding.

`CREATE INDEX` is the SQL command that builds one. (More SQL below.)

------

## 9. Writing good SQL ⭐ (the part you control)

### (a) Optimizer hints (embedded as C-style comments)

```sql
SELECT *  FROM product   /*+ ALL_ROWS */        WHERE ...;   -- get ALL rows fast
SELECT *  FROM product   /*+ FIRST_ROWS */      WHERE ...;   -- EDA: just show table shape
SELECT *  FROM product   /*+ INDEX(qoh_index) */ WHERE ...;  -- use this specific index
```

- The `/* ... */` is a **C-style comment** (SQL dates to ~1985, C-era). A normal parser **ignores** it.
- The **leading `+`** is the **secret signal to the optimizer**: "this comment is a hint for *you*." Without the `+`, it's just a programmer comment the optimizer skips.
- 🚩 **Exam analogy — Java Javadoc:** Java uses `/** ... */` (an **extra `\*`**) so the **Javadoc tool** (not the Java compiler) extracts it and auto-generates **HTML docs with links** from in-code documentation. Same pattern: a special character flags content for a *different* processor.
- **Markup vs Markdown** (related thread):
  - **Markup** = add tags to plain text to enrich it (HTML `<h1>…</h1>`, SQL hints, Javadoc). "You take plain text and add something to make it better."
  - **Markdown** = the lazy inverse — `#` instead of `<h1>`/`</h1>`; a **markdown processor emits HTML**.
  - Agent files (`SKILL.md`, `CLAUDE.md`, etc.) use markdown (machine-friendly). Newer take (Karpathy): **HTML is more expressive** for human-facing agent output (images/graphics), so the pendulum swings back → **HTML vs Markdown** is a real trade-off.

### (b) AND / OR short-circuit ordering

Boolean conditions **short-circuit**; the engine **won't reorder for you**, so order them yourself:

- **AND chain** (`a AND b AND c`) — fails as soon as one operand is **false** → **put the most-likely-FALSE condition first** (skip the rest).
- **OR chain** (`a OR b OR c`) — succeeds as soon as one operand is **true** → **put the most-likely-TRUE condition first**.

**Example** — find students who are CS majors **AND** football players (many CS, very few footballers):

```sql
-- ✅ efficient: rare condition first → most rows fail immediately
SELECT id, first_name, last_name, email
FROM students
WHERE football_player = 'Y' AND major = 'CS';

-- ❌ less efficient: many rows pass `major='CS'` only to fail the AND
WHERE major = 'CS' AND football_player = 'Y';
```

### (c) Don't put math on an INDEXED column (preview — *continued tomorrow*)

An indexed column is **pre-sorted/read**; the optimizer **won't recompute the index** for a transformed expression. **Keep the indexed column bare**; move the arithmetic to the other side.

```sql
-- if column b is indexed:
WHERE a > b * 1.1     -- ❌ math wraps b → b's index is USELESS
WHERE a / 1.1 > b     -- ✅ b is bare → b's index is USABLE   (algebraically identical)
```

**Rule:** the indexed column should appear **alone** on one side of the comparison — no functions/arithmetic around it.

------

## 🎯 Exam flags & one-line takeaways

- **Performance tuning = 3 things only: SQL Cache, Data Cache, Optimizer.**
- **Access plan = compiled SQL** (efficient access route); cached as **hash → plan**; **not portable** across engines.
- **Hash the query key, never the plan** (hashing is one-way; compress the plan instead).
- **Optimizer's 3 dimensions:** Operation mode (**Manual/Auto**), Timing (**Static/Dynamic**), Info type (**Statistics/Rules**).
- **Statistics↔ML, Rules↔Symbolic AI, +Reinforcement Learning = the 3 branches of AI** (the "weird exam question").
- **Index = sorted helper table → binary search; log₂(1B) ≈ 30 vs 1B.** Range search = 2 binary searches.
- **Sparsity:** index **high-cardinality** columns (DOB, GPA, state); **don't** index low-cardinality (gender).
- **Structures:** B-tree **O(log n)** (heap, rebalance), Hash **O(1)** (collisions), Bitmap (one-hot + AND mask).
- **Name-this:** **one-hot encoding** (one bit = 1), **heap** (B-tree property), **markup** (enrich plain text), **Javadoc** (`/**` extra star).
- **Good SQL:** hints `/*+ … */` (the `+` matters) · AND → most-likely-false first, OR → most-likely-true first · keep indexed columns bare (no math).

## 🔜 Next lecture

Finish the optimizer-hints / "no math on indexed columns" examples, then start **Business Intelligence → Data Warehousing → Data Mining** ("BI"): piling all the data into a warehouse (à la Costco) and mining it. *Data mining → machine learning → agents* is one continuum; **any data-mining algorithm is the starting point of ML.**



# 6/17 Lecture: CS585 — Performance Tuning · Business Intelligence · Spatial DBs (Intro)

*Cheatsheet-style lecture notes*

------

## 0. Framing context (pair programming → agentic loops)

- **Pair programming** = software-dev paradigm from the **1990s**. Core idea: one person should **not** do everything (specs → code → unit testing → integration testing → deployment). A solo dev = no checks → wrong architecture, missed tests. So pair one programmer with another; they **take turns** (today I write/you review, tomorrow you write/I review).
- **Why it matters now:** agentic AI coding works the same way.
  - The **agent coding loop**: agent works → comes back "I'm done" → a **checker loop** reviews and gives feedback → agent revises → "check again." Internal back-and-forth.
  - The checker is often an **LLM-as-judge** — *not* the same model/agent; can be a **sub-agent** distinct from the main one.
  - Scale to **3 agents** and quality compounds each iteration.
- **Industry asides (flavor, not exam):** Cursor (started "vibe coding"); rise of open Chinese models (DeepSeek, GLM) with permissive licenses & near-zero cost vs. paid US models; startups building products on top of Chinese models. Mentioned only to motivate why agentic/AI tooling is everywhere.

------

## 1. PERFORMANCE TUNING

Two levels of tuning: **(a) DB/system setup level** (while running) and **(b) SQL/application level**.

### 1.1 Optimization modes (set at system level)

Pick along three axes:

| Axis       | Option A                       | Option B                               |
| ---------- | ------------------------------ | -------------------------------------- |
| How chosen | **Automatic** (system picks)   | **Manual** (programmer rules)          |
| When       | **Static** (one-time, compile) | **Dynamic** (runtime)                  |
| Basis      | **Statistical** (data-driven)  | **Rule-based** (expert-system / logic) |

- **SQL caching**: store compiled access plans so plan compilation isn't re-wasted.

### 1.2 Indexes — the main SQL-level tuning lever

- `CREATE INDEX` on any column(s) you care about — **does NOT need to be a key**. Salary, GPA, date, name, age... any column; can make multiple single-column indexes.
- **Why:** raw table column is unsorted → searching/min/max is **O(n)** full scan. After indexing (sorting), you can do **binary search** or **hardware-accelerated search**.

**Three index implementations (independent — none built on the others):**

**1) Hash index — O(1) constant lookup**

- A **hash function** maps each raw value to a slot ("room number") in a **hash table**.
- Give it the key → it tells you the exact slot in **one fixed-cost step**. No searching at all.
- The slot holds (or points to) the actual raw record you want.
- **Collisions** (>1 value per slot) are allowed.
- *Toy example:* store two-digit numbers (0–99) in a **10-slot** table → hash function = **integer division by 10**. `65 / 10 = 6` (int) → lives in slot 6. Designing a good hash fn = **art of minimizing collisions**.

**2) B-tree index — O(log n) binary search**

- Sorted structure (sorted array, or a tree/**heap**).
- **Binary search on array:** always look at the middle; compare; discard the half that can't contain the target; repeat. Speedup comes because everything is sorted.
- **Heap property** in tree form: for any node, left subtree < node < right subtree (left small, right big).
- **Leaf nodes contain the actual values / row-record pointers.** You don't know the row's location in the main table until the search lands you there.
- Fast, but **not as fast as a hash** (log n vs constant).

**3) Bitmap index — hardware bit-mask / AND**

- No binary search, no hash. Uses a **hardware AND operation** on bit patterns.
- Think **dot product** (like ML vectors): query vector `001` matches only the matching vector (dot product = 1); all others give 0.
- Store bit patterns in a hardware register → bitwise AND → only matching rows return → point to raw locations.

### 1.3 Index selectivity

- The optimizer **won't use every index**. Only index columns that are **worth it**.
- **Worth indexing = many distinct values** (GPA, salary, age). Low-cardinality columns (few distinct values) → index has tiny # of rows each pointing to huge value lists → degenerates back to **linear search → pointless**.

### 1.4 Optimizer hints

- To force a specific index, **embed a comment** the optimizer picks up (e.g., name the index `quantity_on_hand_index`).
- If you hint a **nonexistent** index, query still returns correct results but runs **slow** (full scan).

### 1.5 ⭐ SARGable predicates — literals vs expressions (EXAM-LIKELY)

> "Take your calculator out and divide first."

Scenario: "after I raise every price by 10%, which products cost > $50?"

| Form                     | Index usable? | Why                                                          |
| ------------------------ | ------------- | ------------------------------------------------------------ |
| `WHERE price > 50/1.1`   | ✅ **YES**     | `50/1.1` is a **literal value** → binary search can find it directly |
| `WHERE price * 1.1 > 50` | ❌ **NO**      | LHS is an **expression on the column** → breaks the index → falls back to **full table scan** to compute per row |

- **Rule:** keep the indexed **column simple** on one side, a **literal** on the other.
- **Why the optimizer won't auto-fix the expression:** expression complexity is **unbounded** (arbitrary columns, powers, etc.), so it refuses to pre-compute a new index for it.
- *Simple column* = literally `price`. *Literal* = `50/1.1`. **Mixed** (`price*1.1`, `GPA*1.05`) = **expression** → index gone.

### 1.6 Primary keys

- **Always auto-indexed** by the system → fast lookups (a key reason PKs are useful).
- **Prefer numeric PK over string PK.** Numbers are far easier to hash → better/faster hash functions (e.g., a 10-digit student ID hashes cleanly). Strings have more characters → more complex hash fns.

### 1.7 ⭐ WHERE / AND / OR condition ordering (short-circuit eval)

- **AND chain:** put the condition **most likely to be FALSE first**. First false → whole expr = 0 → **stop immediately**, skip the rest.
  - e.g., "made by rare manufacturer AND price < $10" → check manufacturer first (often fails fast).
- **OR chain:** put the condition **most likely to be TRUE first**. First true → whole expr = 1 → stop.
- The optimizer/ML **can't guess** likelihood — **you** must know your data (distribution / past experience) and order conditions accordingly.

### 1.8 Caches (use high-speed RAM where possible)

- **Data cache** — copies table data; SQL calcs run on it.
- **SQL cache** — holds **access plans** (doesn't strictly need high-speed memory).
- **Sort cache** — used when **building an index** (sorting a column), and for `ORDER BY` / `GROUP BY` results.
- All ultimately = memory; faster memory → faster queries.

### 1.9 In-Memory Database (IMDB) — bypass tuning by brute hardware

- Hold the **entire DB** (all rows/cols) in **RAM** or fast **SSD** (e.g., Samsung T7, ~2 TB, no moving parts → very high transfer rate).
- Then SQL runs fast regardless of tuning.
- **Redis** = key-value (JSON) store; values small enough that whole table fits in memory → "damn fast." (Leads into NoSQL topic.)

### 1.10 Physical storage organization

- **Group commonly-joined / related tables** into one storage volume → joins retrieve from same place.
- Keep **indexes in a separate volume** from data.
- Store **materialized views** (for analytics) separately from base data → heavy analytics/index work won't degrade normal table queries.
- Only **join necessary tables/columns** (no unnecessary joins — common sense).

### 1.11 Access plans & EXPLAIN

- **MySQL** (now Oracle-owned; free for private use, paid "managed" support): good indexing booklet — all about indexing, B-trees, etc.
- **Multi-level index:** index by one column, then by another (e.g., **state then salary**, or **salary then state**). The **primary index** is the column you prioritize; the **secondary** is the other. Order depends on the dominant query type. No limit on # of levels.
- **EXPLAIN** keyword → shows the **access plan** for a query. Plans are **platform-specific** (Mac/Intel/Oracle all differ) even for identical SQL. Experts read & even **manually modify** plans (human optimization).
- **Analogy — inline assembly:** in C, the **`ASM`** directive lets you "poke" raw assembly into C for the critical fast part (e.g., game engines, device drivers). Not portable across CPUs (Intel vs Apple Silicon vs Arduino). Modifying SQL plans ≈ same "best of both worlds" idea. (One level lower = literal 1s/0s, nearly impossible to program.)

------

## 2. BUSINESS INTELLIGENCE (BI)

### 2.1 What BI actually means

- **"Intelligence" = knowledge/information** (as in CIA), **not IQ**.
- BI = "given a massive pile of **past** data, what can I **learn** from it?" = **100% data mining / machine learning** — find patterns to inform future decisions.
- *Examples:* declining water-bottle sales trend → stop selling; rising stock trend → likely keep rising. It's **extrapolation** from the trend.

### 2.2 ⭐ "Facts are friendly" + legal rule

- BI uses **only existing past data** — you **never collect new data** for mining.
- **Never modify past data.** Changing it = lying to investors = a **federal crime**. Facts may be unpleasant, but the number itself is "friendly."
- Need **large volumes** + a **zoomed-out** view; a small/recent slice tells you nothing (e.g., a young PM who only saw the last 10 years can't predict).

### 2.3 ⭐ The BI pipeline = decision support (EXAM: "take a DB, fill it, query it")

```
Sources → [ETL] → Data Warehouse → Query/Analyze → Visualize/Report (dashboard) → ACT
```

- **ETL = Extract, Transform, Load** → into a **Data Warehouse** (the big pile of past data; like Costco stacking goods to the ceiling).
- The point isn't the charts — you must **act** on the insight (= **decision support / data-driven decision making**). Acting on intelligence is the whole point (CIA analogy: act before the bad thing happens).

### 2.4 Operational vs analytical data

- **Operational data** = live micro-transactions, captured by **POS = Point-Of-Sale terminals** (the checkout scanners). Hundreds/thousands of them per chain. "How the business operates," constantly INSERTing.
- Aggregate all operational data into **one place** → the warehouse → then do analysis.
- Data has **many dimensions** (not just 3D) — each **column = a dimension**; can be 30, 100 columns.

### 2.5 Clustering / segmentation

- Plot each purchase as a **dot** in N-dim space (a **scatter plot**) — e.g., axes = age, income, education.
- Dots form **clusters** → run **K-means / hierarchical clustering**.
- Business names: **database marketing / database segmentation / customer clustering.**
- Use: once clustered, a **new customer** is matched to a cluster → served the ads/recommendations that cluster buys → likely to convert. (Same logic as recommendation engines.)

### 2.6 External data

- Events **beyond business control** that still affect behavior: oil prices, elections, assassinations, earthquakes, economic shifts (e.g., small baskets → full carts as money tightens).
- **Store it** so future analysts can **explain** dips/spikes ("there was an election") — provides **context** to the trend.

### 2.7 Batch vs Streaming vs Mobile BI (evolution)

- **Historically:** batch — analyze once or twice a year (limited bandwidth), printed on **mainframe fan-fold ASCII paper**.
- Interval shrank: yearly → monthly → **real-time**.
- **Streaming BI** = analyzing/visualizing **high-velocity data in motion**, continuously (e.g., Amazon dashboards updating live).
- **Mobile streaming BI** = same, consumed on phone/iPad (eventually AR glasses). The phone just **consumes a dashboard**; the cloud does the actual BI.
- Enables instant insights, real-time alerts, automated actions, rapid experiments (e.g., Vans drops a design for one weekend, cuts it if it doesn't sell).

### 2.8 Dashboards & KPIs

- **Dashboard** = many analytics results in one place (**Salesforce** popularized it; also arguably **invented cloud computing** but never called it "cloud").
- **KPI = Key Performance Indicator** — the one/few numbers the boss watches (green = good, yellow = danger, red = crisis). Like a car dashboard; "tell me in 5 seconds how I'm doing."
- **Salesforce Agentforce** = agents that watch dashboards and can alert/call you when something goes bad.

### 2.9 Data marts

- **Data mart = mini warehouse** = a partitioned subset of the warehouse for one product manager / domain (e.g., the "cars" PM doesn't care about "apps & games").
- Same workflow on the subset: query → act, just on limited data. (Banks: separate marts for home loans, car loans, checking/savings, business loans.)

------

## 3. ETL (Extract · Transform · Load)

- **Extract** = grab **only the info you want** (a receipt records cashier name, timestamp, lane #, store # — drop the cashier name *unless* the analysis is HR/performance-related, in which case keep it). = filtering.
- **Transform** = convert all data into **one common format** (the critical step):
  - **Dates:** `4/2` means different things in US vs. EU → don't blindly merge April vs. February.
  - **Currency:** RMB/yuan + euro + USD must be converted to one (e.g., USD) before summing/averaging — else you're adding apples & oranges.
  - *Cautionary tale:* NASA mission failed because most calcs were metric but one was in **miles** (units not transformed). "Obvious" mistakes happen often.
- **Load** = `INSERT INTO` the warehouse table (the easy part).

### 3.1 Schema-on-write vs Schema-on-read

- **Schema-on-write** = make the schema (table) **first**, then fill it (classic; Extract only what the schema wants).
- **Schema-on-read** = **data first, no schema**; dump a pile, **read sample data** to infer columns, **then** build & fill the table.

### 3.2 Tools

- **Informatica** = the classic ETL company (80s–90s); now **owned by Salesforce**.
- ETL jobs ("data plumbing") are abundant & a **soft entry into tech** — SQL is the #1 listed skill (plus Python, Spark, ML). "Do it for a year, then move to ML."

------

## 4. DATA WAREHOUSE

### 4.1 Characteristics (the four standard properties)

- **Subject-oriented** (can be split into marts/domains)
- **Integrated** (everything aggregated into one place)
- **Time-variant** (long history — decades; e.g., Walmart 50 yrs)
- **Non-volatile** ⚠️ — **never modified** ("Why modify the past unless you're covering up?")
- Also: **read-only**, **monotonically increasing** (volume never shrinks unless you delete).

### 4.2 OLAP

- **OLAP = Online Analytical Processing** = warehouse processing.
  - "**Online**" here is legacy (= logged onto a mainframe) → today ~meaningless.
  - "**Analytical Processing**" = the real part = the warehouse.
- Supports **drill-down / roll-up** (microscope: zoom into store-by-store detail, or zoom out to one CEO number).

### 4.3 ⭐ SOX compliance

- **SOX = Sarbanes-Oxley** (two senators). If you do **government business**, you must **retain records ~7 years** for auditing — **cannot delete/destroy** them. Every data point should be **traceable to its source** (provenance / metadata). After the retention window, you may delete to save space.

------

## 5. STAR SCHEMA

```
        [Customer Dim]      [Product Dim]
                \              /
                 \            /
[Time Dim] ----  [ FACT TABLE ]  ---- [Store Dim]
                 /            \
                /              \
         [Promo Dim]        [... more dims]
```

- **Fact table** = the warehouse center. Each **row = one factual transaction** (millions/billions of rows). **Highly normalized** — holds only the **minimum** needed: foreign keys + measures.
  - Typical columns: `customer_id`, `product_id`, `store_id`, `time`, `units`, `unit_price`, `total_price`.
  - These look like PKs but **repeat** (same customer/product/store/time appears many times) → they are really **foreign keys**, collectively a **composite (foreign) key**.
- **Dimension tables** surround the fact table; each **column = a dimension** (hence **multi-dimensional**, not just 3D). They **qualify** the facts = supply additional descriptive attributes.
  - The fact stores only `customer_id`; the **Customer dim** has name, email, club-card history → who to mail coupons.
  - Likewise Product dim (manufacturer...), Store dim (location, manager...), Time dim.
- **Relationship: one-to-many** (one dimension row ↔ many fact rows). One store → millions of sales; one product → bought by millions; one Amazon-Prime ID → appears once in dim, many times in fact.
- **Why "star":** loosely connecting dims around the fact looks like a star.

### 5.1 Slice & dice (the "cube")

- **Slice** = filter along one dimension (e.g., sales at noon, or for product X).
- **Dice** = slice again on another dimension. With N dims you keep slicing (3D cube is just the visualizable case; real data is N-dim).
- **Time & location are hierarchical** — one timestamp is *also* this month / this half-month / 2026 / the 2020s; one store is *also* in CA / Western US. This hierarchy is what lets you drill up/down.

------

## 6. SNOWFLAKE SCHEMA

- Take a **dimension** and **normalize it further** into sub-tables.
  - *Store dim* repeats "Los Angeles, CA, West" thousands of times → split: Store→`city`, then a **city→state** table, then a **state→region** table.
- Creates a **dimension hierarchy** (fractal of small tables).
- **Trade-off:**
  - ✅ Less repetition (more normalized).
  - ❌ More **joins** → slower aggregation. "Sales in LA" = easy (one table); "sales in California" = must join city→state for every city → **extra join → slower**.
- **Balance** how much snowflaking vs. flat star you do.

------

## 7. ⭐ FOUR SCHEMA DESIGN CHOICES (summary)

| #    | Design                                   | Normalization                          | Speed               | Space                 | Notes                                                        |
| ---- | ---------------------------------------- | -------------------------------------- | ------------------- | --------------------- | ------------------------------------------------------------ |
| 1    | **Star**                                 | Fact normalized, dims flat             | good                | good                  | dims around fact                                             |
| 2    | **Snowflake**                            | **Most normalized**                    | slower (more joins) | best                  | dims split into sub-dims                                     |
| 3    | **Fully denormalized fact**              | None — dump all dim cols into the fact | **fast (no joins)** | **wastes most space** | every row repeats "LA, CA, West"; disk is cheap so it's done |
| 4    | **Single-dimension / partial warehouse** | in-between                             | —                   | —                     | warehouse built for just one dim (e.g., product-only or region-only) |

- \#2 = most efficient (cleanest normalization); #3 = least space-efficient but fast. Choice depends on usage.

------

## 8. OLAP ANALYTICS

### 8.1 ⭐ Two kinds of analytics

- **Predictive analytics** = the **future**. "Given the data, what happens in the next 10 years?" (linear regression / neural nets / extrapolation). *Most common ask.*
- **Explanatory analytics** = the **past**. "Why did sales fall 50% over 10 years — why didn't you catch it?" Go back and explain.
- Ideal: don't wait until the ship sinks (predictive) and don't micromanage daily (paranoia) — something in between.

### 8.2 ⭐ ROLLUP vs CUBE (two new SQL keywords — EXAM)

Both = fancy `GROUP BY` over **multiple columns**, producing **subtotals + grand total**.

```sql
SELECT col1, col2, AGG(measure)        -- e.g., SUM(units * unit_price)
FROM   ...
[WHERE ...]
GROUP BY ROLLUP (col1, col2)           -- or CUBE (col1, col2)
ORDER BY ...;
```

| Feature            | **ROLLUP**                           | **CUBE**                                                     |
| ------------------ | ------------------------------------ | ------------------------------------------------------------ |
| Columns subtotaled | only **N − 1** (NOT the last column) | **all N** columns                                            |
| Column order       | **matters** (hierarchical)           | doesn't matter (all used)                                    |
| Output             | subtotal per vendor → grand total    | totals by **every** combination (by month AND by product AND...) |

- *ROLLUP example:* `GROUP BY ROLLUP(vendor_code, product_code)` → for each **vendor**, sum its products, give a **vendor subtotal**; all vendor subtotals add to the **grand total**. (`product_code` = the last column → not separately rolled up.)
- *CUBE example:* same grand total, but you also get breakdowns by **month**, by **product**, by **vendor**, etc. — slice/dice every way.
- **Roll up** = go up / aggregate (big picture). **Drill down** = zoom in / more detail (microscope). One number for the CEO; full breakdown for the PM.
- "L columns" idea: same total (e.g., 10M sales) sliced different ways — by product category, by customer region, by time — it's always the same data, just grouped differently.

### 8.3 MOLAP vs ROLAP

- **ROLAP (Relational OLAP)** = standard Oracle/relational DB; uses normal SQL (`ROLLUP`/`CUBE`). Goes through SQL layer → access plan → OS translations.
- **MOLAP (Multidimensional OLAP)** = **custom hardware**, proprietary storage; build your own N-dimensional **data cube** in lots of **RAM**, poke data directly (no SQL/C++/even OS) → **far faster**.
  - *N-dim array trick (C++):* there's only 1-D memory, so use **pointers to pointers** (a pointer storing addresses of 1-D arrays) → `int** q`. Extend to any dimension via pointers→pointers→…→data.
  - *Hardware lineage:* **Beowulf clusters** (wire many Intel x86 boxes for parallel computing, pre-MapReduce/GPU), now mini versions with **Arduino / Raspberry Pi clusters**.
  - *Analogy:* **high-frequency trading** firms rent space next to exchanges + build the fastest custom machines to shave **milliseconds**. (For MOLAP, ms don't matter — it's about building your own cube.)

------

## 9. MODERN DATA ARCHITECTURES

| Concept                                | What it is                                                   |
| -------------------------------------- | ------------------------------------------------------------ |
| **Data Warehouse**                     | structured data → **ETL** → analyze (classic, schema-on-write) |
| **Data Lake**                          | dump **raw/unstructured** data (tables, JSON, CSV, PDFs, Slack/WhatsApp/tweets/email) — **no schema**. Then extract what you need. |
| **ELT** (Extract, **Load**, Transform) | = **reverse ETL** = **schema-on-read**. Load first into the lake, look at the data, infer schema, then transform. |
| **Lakehouse**                          | Data **Lake + Warehouse combined** — unstructured lake but optimized for warehousing on top. (Bill Inmon — inventor of the data warehouse — wrote the lakehouse book.) |
| **Data Mesh**                          | a **more organized lake** — partitioned into **domains** (ML domain, warehousing domain, etc.); domain-specific lakes. Never fully caught on. |
| **Open House**                         | LinkedIn's open-source data-lake product (their take on the lake). |

- Big shift: databases now often **start unstructured** (dump everything), and structure comes **afterward**.
- **Databricks** — platform spanning BI / data science / warehousing; ships an open LLM **DBRX (DB-X)** on Hugging Face.
- ⚠️ *Prof's repeated warning:* several textbook/slide diagrams have the **ETL/ELT arrows or cardinality reversed** — should be **ELT** from lake → warehouse, and dimension↔fact is **one-to-many**, not the other way. Trust the corrected version.

------

## 10. SPATIAL DATABASES (intro + homework preview)

### 10.1 Core idea

- Almost **everything has a spatial aspect** (a location). An alert (crime, gas station, restaurant) → first question is **"where?"**
- **Spatial data = regular data + a location** (≥ two numbers: **latitude, longitude**). Without lat/long it isn't spatial.
- Build a spatial DB by adding **3 things** to a standard DB (like adding a class with types + methods + an index):
  1. **Spatial data types**
  2. **Spatial indexing**
  3. **Spatial query operations** (calculations)
- Libraries: **PostgreSQL → PostGIS**, **SQLite** (built-in spatial). Every standard DB has a spatial add-on layer.

### 10.2 ⭐ The 3 spatial data types

| Type        | Definition                                                   | Example queries                                              |
| ----------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **Point**   | single `(x, y)` location, **no size**                        | building centroid, each person/soldier; northernmost point, centroid (center of gravity), distance between two points |
| **Line**    | an **array of points**                                       | length of the I-10 freeway; distance from a point to a line (perpendicular) |
| **Polygon** | enclosed area from many points (the actual footprint walked around a building) | polygon **area**; closest point on polygon to a given point  |

- **Axis note:** `x = longitude`, `y = latitude`. So mathematically it's **long-lat** (e.g., **Google Earth** takes `long, lat`), even though we say "lat-long" colloquially.

### 10.3 Spatial indexing & queries

- **Index spatial data** for the same reason as normal indexing — so a "nearest gas station / Indian restaurant" query doesn't scan **every** location on Earth and sort by distance.
- **Two-level calculation:** first approximate shapes as **bounding rectangles** (very fast), then do the **exact shape** math (second level).
- Spatial indexing is **very similar to vector-DB indexing** (RAG retrieval-augmented generation).

### 10.4 Computational geometry (the math underneath)

- The "CG" here = **Computational Geometry**, *not* Computer Graphics. It's the intersection of **CS (algorithms) + geometry** that powers all these spatial calcs (abstracted behind SQL-like APIs).
- **Homework:** walk the USC campus, sample GPS coords of coffee places / libraries / buildings, plot on a map, and write a SQL query for the **convex hull** = the outer boundary polygon enclosing all points (drop interior points, no concave cuts) — computed automatically, not by hand.

------

## 11. Tools name-dropped (worth a look)

- **NotebookLM** (Google) — upload PDFs/audio/images → summaries, flashcards, audio overviews, animations; now writes runnable **Colab code** for the math in your docs (sliders to play with equations).
- **Learn Your Way** (Google) — separate product, same "learn your way" idea.
- **Time-series LLMs** (Google's time-series LM; Apple ML) — treat sequential time data like language tokens; **transformers replace ARIMA / moving averages**; prompt for the next-N-years forecast. As accurate as classical methods, new architecture.
- **Santiago Fernando's reverse job-search tool** (GitHub, free) — feed it your resume → searches Monster/Glassdoor/LinkedIn → ranks jobs you qualify for, auto-tailors resume + cover letter per job, scoring + negotiation help; nothing sent until you approve. Runs on Claude or local **Ollama / Gemma / GLM** (no API cost).
- **Ralph's loop** (a.k.a. **Ralph Wiggum loop**, coined by **Jeff Huntley**) — autonomous-agent pattern that **repeatedly loops the same instructions, one task per loop**, with fresh context each iteration instead of one runaway prompt. "Everything is a Ralph's loop."

------

### Quick exam-flag recap

1. **Literal vs expression** in `WHERE` → keeps/breaks the index (1.5).
2. **AND/OR short-circuit ordering** (1.7).
3. **BI pipeline**: take a DB → fill it (ETL) → query it → **act** (2.3).
4. **"Facts are friendly"** — never alter past data; **SOX 7-yr retention** (2.2, 4.3).
5. **Warehouse 4 properties**: subject-oriented, integrated, time-variant, non-volatile (4.1).
6. **Star vs Snowflake vs Denormalized vs Single-dim** (§7).
7. **ROLLUP (N−1 cols) vs CUBE (all N cols)** (8.2).
8. **Predictive vs Explanatory** analytics (8.1).
9. **3 spatial types** Point/Line/Polygon; `x=long, y=lat`; **convex hull** (§10).



# 6/18 Lecture: CS585 — Spatial Databases (Cheatsheet)

> Topic flow: spatial data → properties → geometric primitives → computational geometry → operations → SQL queries → **indexing** → query processing → implementations → visualization → KML/tools → homework.

------

## 0. Course-Context Asides

- **NoSQL** is "the next big thing." Normally **4 categories**; recently a **5th** added: **vector DBMS**.
- **Vector DBs** started the whole **RAG** idea (the "first RAG type").
- BUT for **agentic AI**, vector retrieval is "slowly going away." Plain text + Unix **`grep`** is often *better* than vector retrieval for text.
  - Vectors shine for **image / audio**. For **text**, chunking a PDF into vectors often **fails** (RAG misses the answer even when the PDF clearly contains it). → more on this next week.
- **Diffusion transformers** are the alternative to autoregressive LLMs (generate all tokens at once, not one-at-a-time).

------

## 1. What Is Spatial Data?

**Definition:** anything that has a **point**, **line**, or **polygon** associated with it. Otherwise it is *not* spatial data.

| Primitive | Property     | "Extent" |
| --------- | ------------ | -------- |
| Point     | **Location** | none     |
| Line      | **Length**   | extent   |
| Polygon   | **Area**     | extent   |

- A salary/GPA column is *not* spatial — but plot employees on a world map and the data **becomes** spatial.
- **Spatial database** = a normal database with **columns that hold points/lines/polygons**.

### Geospatial vs Spatial

- **Geospatial** = spatial data about the **Earth** (latitude/longitude). The prefix *geo* = Earth.
- **Not all spatial data is geospatial**: galaxy clusters, DNA molecules, organs in the body are spatial but not geospatial.
- USC offers a whole **MS in GIS** (Geography dept, online). → Google "GIS jobs" = hundreds of openings.

------

## 2. Key Properties of Spatial Data (don't exist for a GPA column)

### (a) Spatial Autocorrelation

- Loosely = **clustering**. Similar things cluster together.
  - Downtown LA: **flower district, garment district, jewelry district**; **residential zones** are quiet/clustered; **industry/factories** pushed to a separate part of town.
- **High autocorrelation** = data in big contiguous blocks. **Low** = fragmented/broken-up.
- **In LLMs**: autocorrelation ≈ **autoregression** — each generated token is appended to the prompt → vector grows → used to derive the next token → chain grows. (Diffusion does *not* do this.)

### (b) Scale Dependence

- Zooming in/out changes **what data is shown** (the "USC" label vanishes as you zoom out; series/cities drop off until the whole frame is just "California").
- **Only spatial data has this.** A GPA column looks the same zoomed in or out.

### (c) Time Dependence → Spatio-Temporal Data

- Spatial data **changing over time** = **spatial-temporal data**. It evolves; doesn't exist all at once.
- Examples: coastline erosion (water moves 20–30 ft inland over decades; Florida partly underwater), **hurricane paths** (eye moves day by day), Gaza bombing, **Amazon deforestation** (green → brown), disease spread.

------

## 3. Entity View vs Field View

| View            | Meaning                                                      | Used for                                     |
| --------------- | ------------------------------------------------------------ | -------------------------------------------- |
| **Entity view** | Discrete objects — one point = an entity, one building = an entity | **Databases** (discrete math). ← we use this |
| **Field view**  | Continuous space, no singularities ("pass my hand, I don't disappear") | Calculus; **not useful** for DBs             |

------

## 4. 2D vs 3D (z-value)

- `x, y` ≈ longitude, latitude. Add **`z` = altitude** for 3D.
- **Topographic / topographical map** = elevation map (contour lines, each = equal height).
- Rocky Mountains have big z-values; US East Coast ≈ flat. Without z, no topography.

------

## 5. Real-World Domains (every data point has a story)

- **Oil pipelines** — pipe length/diameter + flow rate → time to other side.
- **Agriculture** — micro rainfall maps sold to farmers (helicopters collect data) → plant/harvest decisions.
- **Insurance** — price premiums by distance from river (flood) or forest (fire). *Buffer zone* pricing.
- **Military** — Ukraine/Russia border moves daily; commanders plot the real boundary.
- **Medicine** — body is 3D (MRI: brain top, heart, etc.); **molecular biology** — DNA/caffeine/COVID molecules are 3D (atoms have arrangement; drugs target/break rings).
- **Astronomy** — galaxy clusters = 100% spatial.
- **Disease spread (spatio-temporal):**
  - **Zika** — from Brazil → US South → now everywhere (even CA/LA). Dangerous in pregnancy (shrinks baby's brain).
  - **COVID** — started in Wuhan → worldwide. **Johns Hopkins COVID dashboard** animated daily spread (now frozen).
  - **OxyContin / opioid epidemic** — Purdue Pharma (Sackler family) invented strongest opioid; bribed doctors; started in Kentucky/West Virginia → all 50 states. All state attorneys general sued together.
- **Income / home prices** — use **median, not mean** (a few $50–80M Bel-Air homes / Elon-tier incomes skew the mean).
- **Traffic** — changes every minute (green → "blood red"); Caltrans finds **choke points** → builds on-ramps.
- **Deforestation** — Amazon = "lungs of the planet"; loss of species, culture, oxygen exchange.
- **Crime** — LAPD / crimemapping.com / LA Times Homicide Map; filter by crime type (robbery, DUI, larceny, auto theft); **CompStat** (1970s origin — story for another day).
- **Government agencies** (federal + state + city) must **share spatial data** — it's of "**national importance**":
  - **BLM** (Bureau of Land Management) — federal land out west, lease for ranching (blm.gov).
  - **DOT** — exits, freeways.
  - **EPA** — pollution index + **Superfund** map (buried spent nuclear rods in concrete; still radioactive). Santa Susana / Boeing site near LA still radioactive.
  - **NASA** — many Earth-observing satellites (ocean rise, salinity, cloud cover, infrared, fire maps; **Landsat** = one of the oldest).

### How Spatial Data Is Collected

- **Satellites** — **Maxar Technologies** (Ukraine/Russia imagery; declassified mid-res to public, but **<1 ft resolution still classified**).
- **Drones** — photos → data.
- **LiDAR** — car-mounted (Waymo's spinning top, very local) **or** giant LiDAR for buildings → **point cloud** (full 3D x/y/z), render fly-through video games.
- **Cartography / surveying** — oldest method; camera-on-a-stand measures angles/elevation → contour maps.

------

## 6. Geometric Primitives

- **Point** — location only. Two points → can compute **distance**.
- **Line** — has length; **can self-intersect** (still "length" type, not a polygon).
- **Polygon** — has area.
  - Can have **holes** → the hole = **negative polygon**; the filled part = **positive polygon**.
  - **Golf course example:** subtract the lake (water area) from total → real grass area to buy. Bigger lake = more money saved.
  - Boundaries can be **straight or curved (arcs)** (e.g., round White House).
- **Rectangle shortcut:** specify only **2 corners** — `(xmin, ymin)` and `(xmax, ymax)`. The other 2 derive from vertical/horizontal lines.

### Terminology (all synonyms)

| Group A            | Group B                   | Group C                                 |
| ------------------ | ------------------------- | --------------------------------------- |
| Polygon = **Face** | Line = **Edge** = **Arc** | Point = **Vertex** = **Node** = **Dot** |

### 4th Data Type: Raster

- **Raster** = **pixmap** = **pixels** = SDR raster. A **picture/image** as spatial data.
- Example: the **satellite layer** in Google Maps (Station Fire photo, fire-retardant drop).

### Layers

- Spatial data = stack of **layers**: roads, buildings, **vegetation/parks**, **raster/satellite** — toggle on/off. (Used in the homework.)

------

## 7. Computational Geometry

### Circle through points

- **2 points** → always a line (Euclid), provided the points differ.
- **3 points** → you can **always draw a circle through them, UNLESS collinear** (all 3 on one line).
  - **Method:** take **perpendicular bisectors** of the edges → they all meet at the **circumcenter** (here also called centroid) → compass from there hits all 3 vertices.
  - **Circumcenter can be OUTSIDE the triangle** (for skewed triangles).
- **Incenter** (always **inside**, no matter the shape): meet of **angle bisectors** → gives the **inscribed circle** (smaller circle).

------

## 8. MBR — Minimum Bounding Rectangle

- The **smallest rectangle that touches all sides** of a piece of data ("rubber band converging from all sides until each edge touches"). Works in **3D too** (smallest cardboard box).
- **Store only 2 corners** (bottom-left + top-right).
- **Why?** It's a cheap **first approximation** to complex real data.
- **Point-in-rectangle test = 4 if-statements:** `x > xmin AND x < xmax AND y > ymin AND y < ymax` → all 4 true = possibly close.
- **False positive:** a point passes the MBR test but **fails** the real geometry test (e.g., "10 miles away in Nevada"). That's fine — still cheaper than testing everyone.
- **Two-step rule (core idea, used everywhere incl. indexing):**
  1. **Filter** with numbers/rectangles → throw out clear non-candidates.
  2. **Refine** with real geometry → true positives only.

------

## 9. Spatial Operations / Relations / Functions

(All these words mean the same thing: what you can **do** with spatial data.)

### Operation families

- **Theme / thematic** — tag points by type (gas station, restaurant, hospital, parking).
- **Buffer** (location analysis) — given a line (river), find all addresses within X miles.
- **Terrain analysis** — where does water end up? (**catch basin**, flow analysis).
- **Network / flow analysis** — **Dijkstra's shortest path**. "Shortest" = a **cost function**: distance OR time OR avoid-crime-areas.
- **Distribution analysis / nearest neighbor** — closest collected point to my apartment.
- **Centrality** — a **number per node** = how important it is. Applies to **any graph**, spatial or not.
  - Variants: **eigen, betweenness, closeness, PageRank** centrality (each gives a different value).
  - **Betweenness** (easiest): which single node, if removed, **partitions** the graph (terrorist-network "capture the boss" example).
  - Apply to freeways/buildings → decide where to add on/off-ramps.
- **Measurement** — farthest 2 points, perimeter, direction (e.g., cities northeast of here).

### Predicate Functions (return **boolean** true/false)

| Predicate               | Example (yes/no)                                 |
| ----------------------- | ------------------------------------------------ |
| **Touch**               | Ukraine–Russia border? ✅  India–Russia? ❌        |
| **Inside / contains**   | Vatican inside Rome? ✅  Vatican inside LA? ❌     |
| **Covered by / within** | Golf course within a city ✅                      |
| **Overlap**             | one running inside the other                     |
| **Disjoint**            | Palo Alto a neighbor of LA? ❌ (disjoint)         |
| **Equal**               | same polygon scrambled `ABCD` vs `BCDA` → equal? |

- *Anything returning true/false is a predicate function (CS term).*

### Set Operations (on area boundaries)

| Op                     | Result                                                       |
| ---------------------- | ------------------------------------------------------------ |
| **Union**              | combine into one bigger geometry (middle overlap disappears) |
| **Intersection**       | what's common to both (Korea **DMZ**, India–China line of control) |
| **XOR (exclusive OR)** | union **minus** the intersection                             |
| **Difference (A − B)** | only A's part, not B's. **Not symmetric** (A−B ≠ B−A)        |

### Closure

- **Closure** = geometry **in** → geometry **out** (like SQL table-in/table-out).
- **Preserves closure:** union, intersection, buffer, convex hull, within-distance.
- **Breaks closure:** **length** and **area** (return a single **number**, e.g., "freeway = 2000 miles").

### Method Notation

- `G.equals(g)`, `G.disjoint(g)`, `G.intersection(g)` — `G` = "us"; the argument `g` = the other geometry.
- **Buffer:** `line.buffer(distance)` → still returns geometry (closure preserved; the distance arg doesn't break it).

------

## 10. SQL Spatial Queries

**Build tables with a geometry column:**

```sql
-- County table
name | state | population | shape (POLYGON)
-- River table
name | source_city | length | shape (LINESTRING)
```

> `LINESTRING` and `POLYGON` are what make it spatial. Remove them and it's just plain data.

**Self-join — "which counties touch Contra Costa?"**

```sql
SELECT c1.name
FROM   county c1, county c2          -- two aliases of the SAME table
WHERE  TOUCH(c1.shape, c2.shape) = 1 -- n² comparison
  AND  c2.name = 'Contra Costa';     -- pin one side
```

- Drop the last line → get **all** touching pairs (full n² result).
- Analogous to the e-commerce join ("everything people bought **with** the primary item").

**Cross-table — "which counties does the Mercer River flow through?"**

```sql
SELECT c.name
FROM   county c, river r
WHERE  INTERSECTS(c.shape, r.shape)
  AND  r.name = 'Mercer';
```

- Data is public: download **shapefile (`.shp`)** format (in the homework description).
- **AI can write all this code** for you (build a 2-dropdown app: pick county A + county B → compute touch).

------

## 11. SPATIAL INDEXING ⭐ (core exam material)

**Goal:** find "what's near me" **without** computing distance to every row / sorting all of them. (Same problem as **vector DB** indexing — find nearest embeddings among billions.)

### A. Z-curve / Z-fractal (space-filling curve)

- A **Z** = 3 line segments. Replace **each** segment with another Z → recurse → **fractal**.
- Maps **2D points → 1D Z-line**. Each point lies "near" piece 1, 2, or 3 simultaneously.
- Recurse into smaller Z's = **hierarchy** → drop into deeper levels → ignore most data → land near you fast.
- **Almost nobody uses this.** **Apple's FoundationDB** does (on GitHub). Functions map `(x,y) → z-coordinate` and back.
- **Connection:** this hierarchical descent = **HNSW** (Hierarchical Navigable Small World) used in **vector DBs**. **FAISS** (Facebook AI Similarity Search) does **Approximate** indexing — fast, but **may miss** some vectors.

### B. R-tree (Region tree) — **the dominant structure**

- Approximate data with **top-level rectangles** (the **root may have multiple parents/nodes**, unlike most trees).
- Rectangles inside rectangles inside rectangles, eventually containing the **actual points**. Uses **MBRs**.
- **Rectangles may overlap** — if a region falls in both, just **count it in one** (or both — "forgiving" structure).
- **Search:** test point against top rectangles → descend (North America → US → SoCal → ...). **1 of 3 / 1 of 4** branches → beats **binary search** (which throws away only 50%).
- Variants: **R+ tree**, **R\* tree** (edge-case efficiency).

### C. KD-tree

- Pick the **approximate middle point** = root. Draw an **alternating** perpendicular split: **vertical, then horizontal, then vertical...** (swaps each level).
- **Unbalanced binary tree**; split lines **pass THROUGH data points**.
- Famous **graphics/video-game** algorithm — load only what's near you.

### D. KDB-tree

- Same idea, but split lines **do NOT pass through data points**; divide area into equal areas; **data lives in the leaves**.

### E. Quadtree

- Bound data in **one big square**; recursively split each square into **4 equal squares** (powers of 2: 1024 → 512 → 256...).
- **Empty** quadrant → **no subdivision** (hollow node, don't even store it).
- **One dot** in a quadrant → **leaf**, stop.
- **Throw away 3/4** each step. **Multi-resolution** (big empty squares, tiny dense squares). Used in **image processing**.

### F. Octree (3D quadtree)

- Root has **8 children**, some empty. Subdivide **only where detail exists**.
- Uses: **MRI, video games, liquid/fluid simulation**.
- **Voxel** = 3D pixel ("volume pixel," a little cube). **Stanford Bunny** demo (flat faces → fewer subdivisions).
- Surgeon can **slice** brain voxel data and render the cut face.

**Evolution summary:** R-tree (top) → R+/R* → KD / KDB / Quadtree / Octree. (Z-curve is the niche FoundationDB branch.)

------

## 12. Query Processing — Two-Level Filtering

| Step               | What it uses                     | Output                                               |
| ------------------ | -------------------------------- | ---------------------------------------------------- |
| **1. Filter step** | **Rectangles (MBRs) only**       | Rejects true negatives; may keep **false positives** |
| **2. Refine step** | **Actual polygon/line boundary** | True positives only                                  |

- **Why filter first?** Real polygon/line **intersection** is computationally **expensive** in graphics; rectangle if-statements are cheap. Only do the real test when necessary.
- Same logic scales up: use a rectangle for "California" to know you're in CA not Oregon.

------

## 13. Implementations

**Every DB ships a spatial library** (= add the 3 things: types + operations + indexing, on top of the core engine, sell as add-on):

| DB                        | Spatial library                         |
| ------------------------- | --------------------------------------- |
| **Oracle**                | `SDO_GEOMETRY`                          |
| IBM Informix              | **DataBlade** (Geodetic DataBlade)      |
| SQL Server (Microsoft)    | geometric / geodetic / geographic types |
| MySQL (Oracle-shepherded) | built-in, **free**                      |
| SQLite                    | **SpatiaLite** (`spatialite.dll`)       |
| **PostgreSQL**            | **PostGIS** ← **homework**              |

### Oracle `SDO_GEOMETRY` — Magic Numbers (enumerated constants)

| Code | Type                                         |
| ---- | -------------------------------------------- |
| 1    | point                                        |
| 2    | line                                         |
| 3    | polygon                                      |
| 4    | heterogeneous (mix of points/lines/polygons) |
| 5    | multipoint                                   |
| 6    | multiline (e.g., all roads at USC)           |
| 7    | multipolygon (e.g., all buildings at USC)    |

- **Dimensionality prefix:** `2xxx` = 2D, `3xxx` = 3D (adds z), `4xxx` = **time-varying** (NOT a 4th spatial dimension).
  - e.g., **`3007`** = multipolygon **with building heights**.
- Oracle functions: **`SDO_RELATE`** (touch/overlap), **`SDO_NN`** (nearest neighbor), **`SDO_WITHIN_DISTANCE`**.
- **In practice you'll use Postgres/PostGIS** (friendlier; AI writes the calls). `SELECT *` shows geometry as a Postgres-specific encoded type — don't worry about the raw form.

### Geocoded Database

- Maps **address (apt #, street, city, zip) → GPS lat/long**. Made years ago (addresses rarely change).
- This is how FedEx/Amazon drivers find you. (FedEx routing even prefers **right turns** — faster than waiting on left turns.)

### User-Defined Types

- DB only ships with `float`/`double`. You **define** points/lines/polygons via a **class definition** (C++/Java) — just like making a custom `Student` or `DriversLicense` type. Others already did this for us.

### Zero-Install Option

- **neon.tech** — Postgres + PostGIS **in the cloud**, no install, no disk space needed.

------

## 14. Visualization

- **Choropleth map** — every point on the map has a **value** (e.g., population density).
  - **Classed** = **ranges** (binning/**quantizing**) → flat colors, **hard boundaries**.
  - **Unclassed** = **continuous/diffuse** blended color, **no hard boundary**. Example: **USA Today weather map** (red→hot, blue→cold, smooth).
- **Bubble map** — bubble **size** = proportion (e.g., mean family income; Washington DC anomaly ≈ 6–8× higher).
- **Racial dot map** (2010 / 2020 census) — **1 dot = 1 person**, colored by race. Shows migration (e.g., Hispanic population spread nationwide 2010→2020). (*"Racial" ≠ "racist."*)
- **Megan's Law DB** — sex-offender locations; **radius search** (who lives within X miles). Named for Megan (assaulted/murdered); law mandates public disclosure of released offenders' locations.

------

## 15. KML — Keyhole Markup Language ⭐ (homework)

- **XML-based** with custom tags for **points / lines / polygons / raster**.
- **Drag-and-drop a `.kml` file into Google Earth** → auto-zooms to your data points.
- **KMZ** = **zipped** KML.
- **Origin story:** **Keyhole** = a San Jose company; made the format + a 3D viewer; **Google bought them** → they wrote **Google Earth** (Google itself didn't write it).
- **Structure:**

```xml
<Placemark>
  <name>Starbucks</name>
  <description>A nice place</description>
  <Point>
    <coordinates>longitude, latitude, height</coordinates>  <!-- x, y, z -->
  </Point>
</Placemark>
```

- One file can hold **many** points + lines + polygons together.

------

## 16. Tools & Products

- **ESRI / ArcGIS** — world's best mapping software (on the 10 freeway, hires USC grads). Visualize new buildings, shadow analysis, etc. Putting "**ArcGIS**" on a resume → interviews (LA landlords want apartment **turnover heat maps**, refreshed every 3 months — pure ArcGIS spatial query).
- **OpenLayers** — free JS map library (alternative to **paid** Google Maps API).
- **QGIS (Quantum GIS)** — free, visual **node-based** spatial work.
- **Mapbox / CARTO / GIS Cloud** — online/cloud (some on AWS).
- **FME** — node-based diagram → build spatial apps.
- **Garmin** — old standalone car GPS devices (used embedded Oracle DB).
- Map-dependent apps that **can't exist without a map**: Google Maps, **Waze**, Uber, **Lyft**, DoorDash, FedEx routing.
- **Google NotebookLM** (uses Gemini) — upload lectures/PDFs/YouTube → slides, podcasts, **"Learn Your Way,"** and new **lightweight agentic coding** (e.g., "make an applet with a density slider" → it writes + runs the UI). Secure cloud computer + ~100 curated tools, data analysis/SQL, JSON/image (nano-banana) support.
- **Gemini + Google Maps API** — build map apps; **live API** voice agent ("show me Berlin," castle tours jumping place to place); + Google Earth makes it **3D for AR/VR**.

------

## 17. Homework Spec

- **Collect 13 points:** **1 = your home/apartment**, **12 = campus locations** (distance students: points near where you live/work).
- **End-to-end ("soup to nuts"):** collect data → **input into a database** → **query** → **plot/visualize**.
- Required tasks:
  - **Convex hull** through your points **via SQL**, plotted on **Google Earth**.
  - Build a **KML** file → drag into **Google Earth**.
  - Use **PostGIS** (Postgres) — locally **or** zero-install on **neon.tech**.
  - Use **layers** (toggle on/off).
- **AI is allowed** — have it write the SQL / build the app.
- Real outcome: students got **jobs** from this homework (ArcGIS resume line; landlord turnover heat maps).

------

## 18. Exam / Study Pointers

- **Core:** points, lines, polygons, and **what queries you can run** on them. Everything else is "wrapper functionality."
- Be ready to argue **why an industry uses spatial data** (e.g., **public safety → DPS → CompStat** crime mapping).
- Don't memorize every operation name — just **know they exist**.
- You won't need the full/complex KML reference for the exam.
- **Still left for next time:** covering the world with **pentagons + hexagons** (i.e., hex-grid / S2-style indexing — Uber's approach).



# 6/23 Lecture: CS585 — NoSQL, MapReduce & Spatial DB (Cheatsheet)

> Covers: spatial-DB wrap-up → Big Data / datafication → **NoSQL (4 models + vector = 5)** → JSON/XML → RAG / polyglot persistence → **MapReduce** (GFS, Hadoop, Hive, Pig, Musketeer). Data mining = next lecture. **Exam is Tuesday** — NoSQL + MapReduce + spatial are the core.

------

## 0. Big-picture framing

- **Big Data** had two halves, and they map to the two big topics:
  - *Shape/type of data changed* → tables no longer enough → **NoSQL**.
  - *Volume exploded* → one-machine `SELECT`/for-loop too slow → **MapReduce** (parallel processing).
- (Trivia) **Oracle** laid off ~21,000 (≈160K → 141K), its **first layoffs ever since 1985**, officially citing **AI**; redirecting ~$50B into data centers, funded out of payroll rather than borrowing.

------

## 1. Spatial databases (last slides)

### New column types

Standard SQL types = number, boolean, string (you can compare/query them). Spatial adds **point, line, polygon** — you need a *point type* (like a C++ point class) to put an `(x, y)` in a column. From points you build lines and polygons.

- Math behind spatial calculations (nearest church, distance between two gas stations) = **computational geometry** (branch of math/CS).

### Uber H3 — hexagonal geospatial indexing

- Classic spatial index = **R-tree / region tree** (rectangular).
- Uber covers the globe **like a soccer ball**: **hexagons + pentagons** (library = **H3**). Pentagons fill the gaps (hexagons alone can't tile a sphere).
- **Hierarchical** (like a quadtree): zoom in → smaller cells; zoom out → bigger cells. More cells over dense coastal cities (LA, Bay Area), fewer over rural Central CA.
- Why better than R-trees: rectangles are flat; the world is spherical, so hex/pentagon tiling fits a sphere more naturally.
- **Use:** when you book a ride you sit in a tiny hex → only a **local search** for nearby drivers (no SF driver picks you up in LA).
- **Surge pricing:** index every rider/driver as a point → dot-density clustering shows high-demand cells → charge more. "**Monetize point data.**"
- Roots in **tiling patterns** (Islamic geometric art).

### Convex hull vs. Minimum Bounding Rectangle (MBR) — *exam favorite*

|           | **MBR (bounding box)**                     | **Convex hull**                                              |
| --------- | ------------------------------------------ | ------------------------------------------------------------ |
| Shape     | Rectangle, **always parallel to x/y axes** | Polygon from **existing data points only**                   |
| Vertices  | Can add new corners                        | **No extra vertices**, no concavities                        |
| Tightness | Looser; wasted empty space                 | Tighter                                                      |
| Rule      | Bounds any shape                           | A point that would create a concavity (a "cut") **cannot** be included → that'd be a *concave* polygon (not allowed) |

- Clicking a point **inside** the existing hull → no change; only a point **outside** the hull changes it.

### Subdivision surfaces (graphics tangent)

**Loop subdivision**: split a triangle at its midpoints → 4 triangles; raise the points off the plane → 3D "tent"; recurse → smooth/spherical. (Same "recursive subdivision" intuition as H3.)

### GIS / AI + geospatial

- **GIS jobs** (ArcGIS) have a low barrier vs. FAANG roles that are cutting staff.
- **Gemini API + Gemini Live API**: "grounding with Google Maps," talk to a map in real time (great while driving). Tools mentioned: **GeoLibra** (Wenzhong Chu, Purdue; runs in-browser, reads KML), mapforest/NYC.

------

## 2. Big Data & "Datafication"

- Pre-1990s data grew at a predictable **linear** rate (governments, banks; most people *consumed* data).
- Web era: every retweet / like / purchase / **mouse-hover path** *creates* data → explosion. Not just more rows — the **shape** changed (a Spotify playlist won't fit one table).
- **Datafication** = data that already existed but nobody realized was a gold mine:
  - **LinkedIn** = digitized resumes; **DoorDash/UberEats** = digitized menus; **Uber** = digitized cab dispatch.
  - Once you datafy something, new value appears and you can transform its purpose.
- Sources everywhere: Fitbit steps, **genome/DNA**, Yelp reviews, Google location history, car GPS + road-loop sensors, **Hubble images** (giga-pixel, too big for one machine → must tile → motivates MapReduce), CERN.

**Michael Stonebraker** — UC Berkeley DB prof; wrote **Ingres → Postgres** (biggest open-source relational DB, from Berkeley); **Turing Award** (CS Nobel); now at MIT. His point: tables are great but **one size no longer fits all**.

------

## 3. NoSQL fundamentals

- **NoSQL = "Not Only SQL"** (a.k.a. non-relational / "no tables"). Term dates to ~**1998**. We still use tables for what they're good for (Amazon keeps money in tables) **plus** non-tables for the rest.
- **CAP theorem trade-off:** choose **Availability** (machine never down) vs **Consistency** (same data everywhere). NoSQL leans **Availability**.
- **ACID (relational) vs BASE (NoSQL):**
  - **ACID** → strong consistency: same data everywhere, always.
  - **BASE** = **B**asically **A**vailable, **S**oft state, **E**ventual consistency → temporarily you may read two "sources of truth"; they converge *eventually*.
- **Schema:** NoSQL is "schema-less" → really **loose schema** (rows needn't share all keys, but there's something in common, e.g. a student ID).
  - **Schema-on-read** (NoSQL): the *file* doesn't care about keys/values; the *application* decides what to extract.
  - **Schema-on-write** (relational): `CREATE TABLE` first, then `INSERT`.
- **Scale-out** (add independent nodes — preferred) vs **scale-up** (relational: stack more disk/RAM on one box).

------

## 4. JSON (and XML)

### JSON rules

- **JavaScript Object Notation** — the universal data format. Invented by **Douglas Crockford** (it was JS's object format).
- Always wrapped in `{ ... }`. Format = `"key": value`, comma-separated; **last pair has no comma**. **Keys are always strings** (double-quoted).
- Values: string, number (decimal, +/-, scientific), boolean, **array `[...]`**, **object `{...}`**, null.
- **Table → JSON:** each row = one **object**; column names = **keys**; cell values = values; whole table = **array of objects** (give the array a key = table name).

### Why JSON beats tables

- **Multi-valued attributes for free**: `"langs": ["C++","Java"]` (illegal in a relational cell → would need string-tokenizing or a side table).
- **Missing value**: in a table = `null`; in JSON just **omit the key+value** (jagged objects — not forced rectangular).
- **Denormalized**: all data in one place → **no joins**. One JSON object can replace 3 joined tables.
- **Infinite nesting = the magic**: objects-in-arrays, arrays-in-objects, objects-in-objects, **2D arrays** (e.g. all your lat/long pairs), recursively. This extensibility is JSON's superpower.
- **Limitation**: keys repeat in every object (duplication). Workaround: list keys/metadata once at top, then rows as plain value arrays (more efficient — looks table-like).

### Grammar

- Described by **BNF (Backus–Naur Form)** / railroad diagrams. **John Backus** (invented Fortran) → BNF formally describes language syntax. Every language (Python/Java/C++) has a BNF; valid programs satisfy it. JSON isn't code but satisfies its grammar.
- Every language has a **JSON parser**: reads file → returns a dict/object of keys+values → you analyze it. (You *can* analyze JSON with your own code, but joining/looking up across multiple JSON files gets painful → that's why **MongoDB/CouchDB give a SQL-like API** instead.)

### XML

- Same idea, 100% inter-convertible with JSON. Uses tags `<tag>value</tag>` — key written **twice** (open + `/close`) → verbose/ugly, 2× to type/store/transmit/parse. **Nobody starts a new DB in XML today**; it's a legacy artifact.

------

## 5. The four NoSQL models (+ vector = the 5th)

| Model             | Examples                                  | Stored as              | Search                    | Notes                                        |
| ----------------- | ----------------------------------------- | ---------------------- | ------------------------- | -------------------------------------------- |
| **Key-Value**     | **Redis**, DynamoDB, Voldemort, memcached | keys+values **in RAM** | **none** (no deep search) | values stay *simple* → fits memory → fastest |
| **Document**      | **MongoDB**, CouchDB                      | JSON/BSON **on disk**  | **deep search**           | values can be complex/nested                 |
| **Column-family** | **Cassandra**, HBase, **BigQuery**        | column-optimized       | column aggregates         | great for column sums/averages               |
| **Graph**         | **Neo4j**, FlockDB                        | nodes + edges          | node-to-node traversal    | most schema-free; represents anything        |
| **Vector** (5th)  | **Pinecone**, Weaviate, Qdrant            | float vectors          | cosine similarity         | for images/audio/video; weak on text         |

### (1) Key-Value

- **Redis** (in-RAM → very fast), **DynamoDB** (Amazon), Voldemort (Facebook), **memcached** (ships with Unix/Mac). Used for game servers, **Amazon shopping cart**.
- Values kept **small/simple** (no deep nesting) so everything fits in main memory → speed.
- **API = `put` / `get` / `delete` only.** No deep search, no "scan all values," no transaction mgmt; usually single-user.
- Can store the same key with **multiple timestamps** (e.g. a book's price on different dates → find the discount sweet spot).
- DynamoDB keeps **N = 3 replicas** (1 fails → 2 backups). (Redis HQ: Univ. Ave near Stanford.)

### (2) Document

- **MongoDB** (most popular), **CouchDB**. A **document = a JSON object** (can be huge: a whole blog post with title, author, JPEG ref, claps, comments nested as objects-in-objects). 100 posts = array of 100 objects; many authors = objects keyed by author.
- Same *structure* as key-value **but**: values may be complex, stored on **disk**, and you get **deep search** — query any field (title/body/author/**comments**) across millions of docs (e.g. articles 2020–2025 with >30 comments).
- Storage: JSON → **BSON** (binary JSON: compact, not human-readable, lossless; API restores it).
- **Query API ≈ SQL** (uses `$` for variables). Supports: `insert`, `find` (simple or complex), **full-text search**, column-style **aggregates** (avg/sum as if columns), **geospatial** (bounding box, **GeoJSON**), **range search** (date/GPA/salary), plus `sort`/`limit`/`skip`.
- **`eval()`** (JS): takes a string and runs it as code with **no checking** → powers custom **map functions** → **biggest security risk** if misused (only internal engineers can do it). Lets you run **MapReduce inside MongoDB** (supply your own JS map + reduce/aggregate).

### (3) Column-family / Column DB

- **Cassandra** (Facebook), **HBase**, **BigQuery** (Google/GCP). Looks table-ish but **optimized for column math** (sums/averages) rather than row `SELECT`s.
- Primary key still exists, now called the **row key** (no foreign keys → just "key").
- **Super column** = one extra hierarchy level: a super-column's *values are column names* which then hold data (e.g. `grad columns` {major, gradDate} vs `undergrad columns` {school, GPA}).
- **API**: `insert` one row, `get`/query, `delete` row — mildly SQL-like.
- **CQL (Cassandra Query Language)**: SQL-ish but **no JOIN / GROUP BY / ORDER BY**; everything is JSON under the hood. `keyspace` = database; `SELECT * FROM monkey` → **returns raw JSON** (the table *is* JSON).
- Underlying structures (review in last class): **SSTables** (Sorted String Tables), **LSM trees** (Log-Structured Merge).
- **Apple runs Cassandra in iCloud.**

### (4) Graph

- **Neo4j** (biggest), FlockDB (Twitter), GraphX/Giraph (Apache). **Most schema-free** — can model tables, docs, key-value, columns, anything.
- A CS graph: may have **cycles**, **directed** edges, **weighted** edges. **Data lives in BOTH nodes and edges** (e.g. LA→Palo Alto edge holds driving distance 530 mi / drive 5 hr / fly 1 hr — *multi-edges* allowed).
- Terminology (all interchangeable): **node = vertex = point**; **edge = wire = arc = relationship**.
- Use: social graphs, recommendation ("bought X also bought Y"), maps (cities within N miles), **IMDb** (actors↔movies). **No indexing** — you hop node→node→node ("non-indexable").
- **Hypergraph** = graph of graphs. **Hypercube** = two cubes wired together. Dimension ladder: **0D=point, 1D=line, 2D=square, 3D=cube, 4D=two wired cubes**. (History: Intel hypercube; **BBN Butterfly** — Bolt Beranek & Newman, among the first 5 ARPANET nodes — a massively-parallel machine wired as a butterfly graph.)

**Graph query languages**

- **Cipher** (Neo4j; *neo/cipher* = Matrix joke) — proprietary, much cleaner than SQL joins. e.g. `MATCH` relationships of type "person → employee_of → department," return the employee names ("like how you think"). Has a JDBC driver (looks like JDBC, but it's Cipher).
- **Apache TinkerPop / Gremlin** — open-source, portable (Neo4j or any graph). "**Gremlin**" = a node; **function chaining** with `out()`: find node `name = gremlin` → `out()` = friends → `out()` again = friends-of-friends. Functional; one jar file; does **centrality, shortest path, cycle detection** (e.g. blockchain), Dijkstra. The closest thing to "SQL for graphs."

**Serializing graphs**

- Any graph → **valid JSON** (multiple ways) — useful for knowledge graphs / agents.
- **DOT** notation: predates JSON ~20 yrs; `A -- B` (undirected), `A -> B` (directed); used in LaTeX. **GraphML** = graph spec in XML (verbose).

**Triple store / RDF — \*important for knowledge graphs + agents\***

- Any graph = a set of **triples**, **3 pieces at a time**: **Subject — Predicate — Object** (e.g. *LA — hasSchool — USC*). Subject/object are reversible (predicate becomes its inverse).
- Store in a **3-column table** (subject | predicate | object). **RDF (Resource Description Framework)** = the XML format for triples (e.g. *person2 — hasChild — person13*).
- Enables **chained logical inference**: mammal ⊃ human ⊃ man/woman ⟹ man/woman ⊂ mammal. This is **symbolic AI / GOFAI / predicate calculus** — humans define relations, no data, "purer" AI.
- **Neuro-symbolic AI** = combine symbolic + ML (recent USC conf, Amazon-sponsored); the idea that scaling-only (pure "neuro") is dead.
- **Native store** (triples directly in XML) vs **non-native store** (in a table). Query langs: **SPARQL** etc. Vendor: AllegroGraph ("semantic platform" vs keyword search).

### (5) Vector database (the new 5th model)

- **Pinecone** (made it popular, serverless), Weaviate, Qdrant, Milvus, Chroma. Each datum = a **vector of floats**, possibly **100s of dimensions** (e.g. dictionary of 50K words → many dims).
- **Train an embedding model** (neural net + backprop): if a cat's embedding lands in the wrong place, the **angle** is used to *punish*; weights adjust until cats cluster here, dogs there. After training, billions of cats/dogs cluster; a new query embeds and does **similarity search**.
- **Cosine similarity**: `dot(a,b) = |a||b|·cos θ`; with unit vectors → just **cos θ**. `cos 0° = 1` (identical/closest), `cos 90° = 0` (dissimilar). Return the vector with the **smallest angle**.
- **Great for images/audio/video** (Shazam-style); **weak for text** because of the **chunking problem** (how much text per vector — line? paragraph? chapter? — kills answer quality).
- **Index = HNSW (Hierarchical Navigable Small Worlds)** — like an R-tree: start coarse, get denser each level, reach your neighborhood in a few hops (scales to billions).

------

## 6. RAG, polyglot persistence, vendor convergence

### RAG (Retrieval-Augmented Generation)

- Leave the pretrained LLM alone; tell it "go find the answer in my external DB."
- **Vector RAG** (first attempt) — weak; by **2026 considered "almost dead"** for text.
- **Graph RAG** — knowledge graph; **superior for text** (a "recursion" chapter holds all the facts → almost always right). Neo4j popularized it; LLM-agent wikis use graphs.
- **Hybrid RAG** = vector + graph. Today there are ~**10 RAG types** — even a SQL query or a Google search counts; "RAG" now just means "go find what I want." (Vectorization still wins for *similarity*, but people are returning to HTML/markdown/plain text.)

### Polyglot persistence

"Polyglot" = many languages, "persistence" = database → **don't commit to one model**. Example e-commerce app:

- Shopping cart → **key-value**; analytics & activity log → **column**; product catalog (one rich item) → **document**; "frequently bought together" → **graph**; financial data → **relational**.

### Vendor convergence (*key takeaway*)

- **Postgres** (~30 yrs old) added **PostGIS** (spatial) and **pgvector** (vectors). Adding vectors to a DB you already run beats running a separate vector-only DB → pure vector startups may not last.
- **MongoDB, CouchDB, Neo4j** all retrofitted vector support. `CREATE VECTOR INDEX` (SQL-like) auto-launches **HNSW**; keep document + vector data in **one search space** (vs. searching separately and merging). All available as simple `pip install` modules.

------

## 7. MapReduce

### Core idea

- Parallel data processing: **same data, same result, but 1,000–100,000× faster** (a day = 86,400 s → "1 second vs. tomorrow").
- Parallel processing dates to the **1950s**; **MapReduce is Google's specific invention** — and it was built **for Google Search**, not databases (search was collapsing as the web exploded → invent it or go out of business).
- **Map** = run the same function on data pieces **in parallel**. **Reduce** = combine the partial results. (Full pipeline: **Map → Combine → Shuffle → Reduce**.)
- **Analogy:** tear a thick book into pages, give one page each to many people, all count vowels A/E/I at once, shout totals to one reducer who sums them → near-unlimited speedup. Or: average salary on Earth = horizontally fragment the table across 6 machines, each computes a **partial sum**, send 6 numbers to one reducer who adds + divides → 6× faster.

### Key mechanics

- **Horizontal fragmentation/partitioning** = break ONE table into pieces across machines (**not** replicas).
- Each map task emits **intermediate (key, value)** pairs; every item emits **`(word, 1)`** (value always 1). **Initial/input keys are dummy** — the *data* is the value; you count occurrences.
- **Shuffle / shuffler** = a separate machine that **decouples** mappers from reducers (don't hard-wire reducer IPs!). It groups all values by key (all "A"s → one reducer; all "E"s → another). CS maxim: **"insert one level of indirection in the middle."**
- **Combiner** = *optional local reduction* at the mapper (sum two local "C"s before sending) → cuts network bandwidth.
- **No fixed mapper:fragment ratio** (e.g. 6 fragments, 3 mappers — one mapper handles 2).

### SIMD vs MISD

|            | **SIMD**                                          | **MISD**                                                     |
| ---------- | ------------------------------------------------- | ------------------------------------------------------------ |
| Meaning    | **S**ingle **I**nstruction, **M**ultiple **D**ata | **M**ultiple **I**nstruction, **S**ingle **D**ata            |
| This is    | **MapReduce** (same map fn, many data fragments)  | **opposite** (e.g. self-driving car: same lidar data → many TPUs, one finds signs, one finds pedestrians) |
| Difficulty | easy ("dumb": run one fn on data)                 | hard (must know what's parallelizable; TensorFlow graph)     |

- **Speedup is sublinear** (N processors ≠ N×) because shuffle/reduce takes time → **Amdahl's law**.

### Google File System (GFS)

- 2003 papers. People: **Sanjay Ghemawat** (on *both* GFS + MapReduce papers), **Jeffrey Dean** (MapReduce).
- **GFS abstracts file-system/distribution details away from Google's own engineers.** Before it, **NFS (Network File System)** required Unix gurus to mount volumes.
- Flow: **Application → Client → GFS Master → Chunk Servers** (can be 1,000s–100,000s). Engineer just submits map+reduce to the master; distribution is hidden → huge productivity.
- *(Tangent)* **Timnit Gebru** — Google Ethics ("canary in the coal mine") found biased data (white-male faces ~90% accurate, Black-female ~10%). Told not to publish; invoked academic freedom; **fired (~2020)** by Jeff Dean's org; her manager **Margaret Mitchell** also forced out → they founded **DAIR** (Distributed AI Research).

### Hadoop

- **Open-source MapReduce** (Apache) — 100% the same idea (only Google's internal version is literally called "MapReduce"). Built by **Doug Cutting & Mike Cafarella** at **Nutch** (the other search co. about to fail; read Google's paper, implemented it the next year).
- **Name:** Doug's toddler had a stuffed elephant named "Hadoop" (now in a computer museum).
- Run it on **AWS / GCP / Azure** clusters. **YARN = MapReduce v2:** v1 couldn't loop/backtrack or auto-recover from crashes; **v2 can** (massive for-loop + automatic fault tolerance). **No v3.**
- Google uses MapReduce everywhere: Search, Google Docs, YouTube, Maps.

### Higher-level languages on Hadoop

- **Hive = distributed SQL.** Write simple SQL on a "small table" → the Hive compiler analyzes it and **auto-generates map+reduce** to run on the real fragments. SQL becomes an auto-parallelized front end.
- **Pig (Pig Latin)** — Yahoo; a **data-flow language** (data flows through a graph). The Pig compiler turns the graph into mappers/reducers (high-level, like Keras/PyTorch sit above TensorFlow). *Mary-had-a-little-lamb* word count ≈ **4 lines**: load → `FOREACH ... GENERATE FLATTEN(TOKENIZE(line)) AS word` → `GROUP words BY word` → count/dump.
- **Musketeer — the M×N → M+N trick.** M front-ends × N back-ends would need **M×N translators** (each front-end paired to each back-end; e.g. Hive only runs on Hadoop). Musketeer adds an **abstract intermediate graph**: write **one** translator front-end→graph (×M) and **one** graph→back-end (×N) → **M+N** translators (linear, not N²). Same "level of indirection" idea.

### Word-count code

- **Java** (~40–56 lines): subclass `Mapper` (`TokenizerMapper extends Mapper`) → `map()` emits `(word, 1)`; subclass `Reducer` → `reduce()` sums the 1s; `public static void main` wires the classes; compile to `wordcount.jar`; run with input/output dirs.
- **Python**: fewer lines, same for-loop logic.
- Both are **low-level** — prefer Pig/Hive and let translators do the work ("don't write assembly when you can write C++").

------

## 8. People & trivia (quick recall)

- **Michael Stonebraker** — Ingres/Postgres, Turing Award; "tables aren't enough."
- **Douglas Crockford** — invented JSON. **John Backus** — Fortran + BNF grammar.
- **Sanjay Ghemawat** (GFS + MapReduce) & **Jeffrey Dean** (MapReduce). **Timnit Gebru / Margaret Mitchell** → fired → **DAIR**.
- **Doug Cutting & Mike Cafarella** — Hadoop (named after a toy elephant).
- **Oracle** — first-ever layoffs (~21K) citing AI; ~$50B into data centers.

------

## 9. One-screen cheat tables

**ACID vs BASE**

- ACID → strong consistency (relational). BASE → **B**asically **A**vailable, **S**oft state, **E**ventual consistency (NoSQL).

**CAP** → pick Availability vs Consistency; NoSQL picks **Availability**.

**Schema** → relational = schema-on-**write**; NoSQL = schema-on-**read** (loose schema).

**Scale** → NoSQL = scale-**out** (more nodes); relational = scale-**up** (bigger box).

**5 NoSQL models** → Key-Value (Redis) · Document (Mongo) · Column (Cassandra) · Graph (Neo4j) · Vector (Pinecone).

**MapReduce pipeline** → **Map → Combine → Shuffle → Reduce**; model = **SIMD**; speedup **sublinear** (Amdahl).

**Stack** → GFS (file system) → MapReduce/Hadoop (engine) → Hive/Pig (high-level) → Musketeer (M+N translation).

**Postgres extensions** → PostGIS (spatial) · pgvector (vectors).

**Spatial** → types: point/line/polygon · index: R-tree vs **H3 hexagons** · **MBR** (axis-aligned) vs **convex hull** (existing points, no concavity).



# 6/24 Lecture Notes — Big Data Frameworks + Data Mining / Machine Learning

> Cheatsheet covering two big blocks: (1) the **MapReduce ecosystem** of distributed processing frameworks, and (2) a rapid tour of **data mining / ML algorithms**, ending with a deep dive on **neural networks & backpropagation**.
>
> *Garbled names from the transcript are silently corrected here (e.g. Pregel, Giraph, Vapnik, ADALINE, Suno).*

------

## PART 1 — BIG DATA PROCESSING FRAMEWORKS

### 1.1 MapReduce (review)

- **Problem:** Data too big for a single `for` loop.
- **Solution:** Break data into many pieces (**horizontal fragments**) → process each piece **in parallel** → that's where the speedup comes from.
- Each fragment produces a **partial answer**; you combine them with the **reduce** operation.
- You write two functions: **`map`** and **`reduce`**.
- **Naming gotcha:** *Inside Amazon* it's called **MapReduce / EMR**; *everywhere else (open source)* the same thing is called **Hadoop**.

### 1.2 Higher-level frameworks: Hive & Pig

- Writing raw map/reduce is **too low-level**. **Hive** and **Pig** let you express what you want at a higher level:
  - **Hive** → SQL-like queries.
  - **Pig** → Pig Latin scripting.
- A **compiler** analyzes your query and **auto-generates the map and reduce functions**.
- **Analogy:** You *could* program in assembler, but you don't — it's too hard (you'd need to know the memory layout). Instead you write C++ and the compiler maps it to the chip. **Same idea**: map/reduce is the assembler; Hive/Pig is the high-level language.

### 1.3 Musketeer

- An architecture that lets **many front-end graph/dataflow systems** run on **any backend** execution engine (decouples the front-end language from the backend engine).

### 1.4 Cloud + Elasticity

- MapReduce/Hadoop runs on all three major clouds: **AWS, Google Cloud, Azure**.
- **Elastic Cloud Computing:** You tell the cloud a **min** and **max** number of mappers (e.g. min 10, max 100). It **scales elastically** between them based on demand — you won't pay for 1000 if you only need a few.
- **AWS EMR = Elastic MapReduce** — "elastic" because the number of mappers goes up and down.
  - EMR Serverless, data lakes; runs open-source frameworks (**Spark, Presto, Hive**).
  - Provision clusters of any size; each node = a **mapper**.
  - Pitch: "just bring/upload your data + give us your map function, leave the rest to us."

### 1.5 Spark

- **Same core idea as MapReduce**, BUT the fragment data lives in **high-speed main memory (RAM)** or fast SSD, not on disk.
- **RDD = Resilient Distributed Data** — one piece of RDD ≈ one fragment.
- **Key takeaway: faster than Hadoop** because it runs in-memory (often **10×–20× faster**).
- Came from **UC Berkeley**.
- Front-end SQL-like queries get **compiled into map/reduce** under the hood.
  - Spark's SQL engine **used to be called Shark** (an alternate Hive).
- **PySpark** = Python interface to Spark.
- Spark can also do **ML, SQL, graph analytics** — all on top of the map function.
- **SVM example:** the Spark version of an iterative training loop is only ~5–6 lines and runs ~10–20× faster than the Hadoop equivalent (memory speedup).
- **Geek joke:** in "the SVM paper," the last **M stands for "Mouth"** → read the paper **straight from the originators' mouth** (UC Berkeley authors), not 2nd/3rd hand.

### 1.6 Flink — "MapReduce++"

- Like MapReduce but with **extra operators beyond just map/reduce**: `join`, `group`, `filter`, etc.
- In plain MapReduce, mappers can **only** send output to reducers — you **cannot** split a mapper's output into two pieces, do extra work, then rejoin. **Flink can.**
- Used in production worldwide.

### 1.7 Storm + Kafka — data pipelines

- **Storm:** processes a **topology** = a graph of operations. Some ops run in parallel, some in serial. A Storm "graph manager" still writes mappers/reducers underneath, but the topology is a **separate graph** (a *graph of graphs*).
- **Kafka:** message **routing** like a post office. Knows what each **producer** emits and what each **consumer** wants, and routes by **key** (send key "A" this way, key "B" that way).
- **Together:** Storm topology emits different keys → Kafka routes them → feed into other topologies. Endless chaining = **complex data pipelines**.

### 1.8 Samza (LinkedIn)

- Built by LinkedIn to **search through resumes** at scale.
- Resumes stored as fragments; a parallel platform lets **employers query** all resumes simultaneously (e.g. "GPA > X AND CS degree AND graduated") → qualified candidates get filtered out.
- Essentially a **mini-MapReduce for resumes**, with Kafka-style tables (e.g. a "Product Managers" table is populated by scanning all profiles).

### 1.9 Batch vs Stream — which framework does what

| Framework  | Batch (file-based) | Stream (online) |
| ---------- | ------------------ | --------------- |
| **Hadoop** | ✅ only batch       | ❌               |
| **Storm**  | ❌                  | ✅ only stream   |
| **Spark**  | ✅                  | ✅               |
| **Flink**  | ✅                  | ✅               |
| **Samza**  | ✅                  | ✅               |

- **Batch** = the fragment is a file on a file system.
- **Stream** = data online only, nothing goes to disk → faster.
- All of them are **far faster** than not parallelizing at all.

### 1.10 BSP — Bulk Synchronous Parallel (the *true* alternative to MapReduce)

- Everything above is "still basically MapReduce." **BSP is genuinely different.**
- **Key difference:** in MapReduce, mappers **never** talk to each other. In BSP, **mappers (processors) exchange data with each other**.
- Mechanics:
  - Processors P1, P2, P3 do local work (a map-like step).
  - At a **barrier**, all must **synchronize** — none can finish until they've **exchanged the required data** with each other.
  - After the barrier, they continue independent work, then hit a **new barrier**, exchange again, repeat.
- **Why needed:** scientific problems like **matrix inversion** of a giant (e.g. million × million) matrix — you can't just split it into independent pieces; processors must **exchange coefficients**.
- **Human analogy:** "let's not constantly bug each other — go work separately for two hours, then meet up and sync."
- **2026 analogy:** This looks **exactly like agent orchestration** — agents do independent work, then "talk to each other." (Prof calls programming this *goal engineering / loop engineering*.)
- **History:** BSP, **Leslie Valiant, 1992** (same researcher who worked on clock synchronization in distributed computing).

### 1.11 Pregel + graph theory origin (Google)

- **Pregel** = Google's BSP implementation, built for **graph processing** ("graph operations that happen to be parallel" → a dependency graph where some nodes run in parallel, then must exchange data).
- **Why the name "Pregel"?** → **Graph theory's origin story:**
  - All of graph theory (vertices, edges, Prim's, Kruskal's...) traces to **Leonhard Euler** (Switzerland).
  - City of **Königsberg**; the **Pregel River** flows through it, creating **4 parts of the city** connected by **7 bridges**.
  - The mayor asked: *can I walk all 7 bridges exactly once and visit all 4 parts?*
  - Euler proved **NO** → and **invented graph theory** to do it.
  - **Euler's rule:** if any single vertex has an **odd** number of edges, the tour is impossible. (Need **even** degree everywhere to enter-and-leave cleanly.)
  - Footnote: WWII bombing destroyed some bridges → today an Eulerian tour *is* possible (you can check on Google Earth).
- *(Aside: "Seven Bridges Road" is also an Eagles song — prof harmonized a verse.)*

### 1.12 Giraph, GoldenOrb, HPC

- **Apache Giraph** = open-source BSP/Pregel implementation (name = "graph" → "giraffe" pun). Runs like a distributed file system (looks like Hadoop because even BSP's map part can be fragmented).
- **GoldenOrb (GPS)** — another BSP-style graph processor.
- These run on **HPC (High Performance Computing)** / scientific computing: **weather simulation, DNA sequencing, material/fracture simulation, nuclear-bomb simulation** — supercomputer-class problems.
- **Facebook** used Giraph: **~1 trillion edges** (as of ~2015) across its social graph; with billions of users, now likely **many trillions** of edges.

### 1.13 Graph partitioning problem (why BSP matters)

- **You cannot cleanly fragment a graph** — splitting it always **breaks edges/connections** between the pieces.
- A graph split into two pieces is **partitioned** → becomes effectively a **bipartite** situation across the cut.
- The pieces can be **mapped in parallel**, BUT because you broke connections, the nodes must **communicate across the cut** → **this is exactly what BSP enables**.
- Bottom line: **a graph is not the same as rows/columns of data**; it can't be trivially sharded.

### 1.14 MapReduce — why it still matters

- Google uses MapReduce for **everything**: Google Maps, Google Drive, Google Docs, YouTube, search, etc. — because it **speeds everything up**.
- **Agents** can now write the map functions directly and even run them — but **the underlying architecture stays the same**. AI makes it run faster, it doesn't make MapReduce obsolete.

------

## PART 2 — DATA MINING / MACHINE LEARNING

### 2.1 What "mining" actually means

- **Core idea:** extract a **pattern** from data. **The pattern = the model.** (In physics, the model is called an "equation/law.")
- **Golden rule:** **Data → Model. One direction only.** You always fit the model *to* the data, never the reverse.
- **Physics analogy (the whole intuition):**
  - Drop a rock from different building heights; record **height (s)** vs **time to fall (t)**. Pure data, no theory.
  - The pattern is captured by: **`s = ½ · g · t²`** (g = gravity ≈ 9.8 m/s²).
  - That model is **universal** (works on Mars, other galaxies) → it becomes **predictive**: plug in a new height, take the positive square root, predict the fall time.
- **Once you have the model, you can throw the data away** — the model is a **proxy** for the data and can predict **new** things. (Same for a trained neural net or a regression line.)

### 2.2 Predicting from the past

- A trajectory through your **past data** can predict the **future**, **absent any big life-changing event**.
- *(Tie-in to Pirsig's "Zen and the Art of Motorcycle Maintenance" — looking back, the past trajectory explains where you are; data mining does the same.)*
- **Recommended reading mentioned:**
  - **Richard Feynman — \*The Character of Physical Law\*** (where constants come from, why nature is the way it is).
  - **Robert Pirsig — \*Zen and the Art of Motorcycle Maintenance\*** (on **"quality,"** philosophy, existence).

### 2.3 Trends & stale models

- **Trend** = pattern over a **time axis**; can be non-monotonic (wiggle up/down) but have an overall direction.
  - Example: water-bottle sales cyclical by season but overall **declining** → eventually stop selling.
  - **Global warming** = an overall **rising** trend; cherry-picking a tiny dip to claim "it's fake" is the classic mistake — **zoom out** to see the real trend.
- **Data mining is a cyclical, never-ending process:** collect → model/mine → act in the world → that changes the data → re-model. Stop and your competition catches up.
- **Stale model:** old data no longer represents reality (e.g. a 20-year-old regression line, or a neural net trained on outdated data). Must **re-model / retrain**. (Even "attention span" shifts year to year, invalidating old models.)

### 2.4 ML vs Data Mining

- **Basically the same thing** — same algorithms.
- Subtle difference: in **ML**, the machine learns the pattern **autonomously** and acts (especially **agents**); in **data mining**, a **human** uses the resulting model.
- A neural network is **both** ML *and* data mining.
- **History:** **Andrew Ng** popularized the term "machine learning" with his **Stanford course** put on the internet (~30,000 enrolled in week 1). It started with **linear algebra (dot products, vectors, matrices)** → enrollment dropped like a rock when people realized "it's math." He went on to **co-found Coursera**.

------

## PART 3 — THE 4 ALGORITHM TYPES + SUPERVISED/UNSUPERVISED

### 3.1 Every DM/ML algorithm (even LLMs) is ONE of four kinds

| Type               | What it does                                  | Output                                          |
| ------------------ | --------------------------------------------- | ----------------------------------------------- |
| **Classification** | **Labels / names** data                       | A label (e.g. "chair," "good wine," "$X price") |
| **Clustering**     | **Groups** data into clusters                 | Group membership (clusters have **no names**)   |
| **Association**    | Finds **relationships** — what goes with what | "A is bought with B"                            |
| **Regression**     | Fits a **mathematical equation** through data | An equation / curve                             |

- **Classification vs Clustering** (the key distinction):
  - Classification → **labels have names** (often), data has a distributional structure per label.
  - Clustering → just **groups**; clusters have **no names**, no per-label distribution.

### 3.2 Supervised vs Unsupervised

- **Supervised:** past data has a **label column** (you mark answers) used as **training material**.
  - Examples: image classifier (1000 cat photos all labeled "cat"), bank-loan default predictor.
- **Unsupervised:** **no labeling** of the data.
  - Examples: **clustering**, and **LLMs** (you feed raw English; you don't tag every word as noun/verb).

------

## PART 4 — ALGORITHM-BY-ALGORITHM

### 4.1 Decision Tree (Classifier) — C4.5 / C5.0

- Build a **tree** (root → leaf nodes) from the **columns** of past data. **Leaf nodes = decisions.** Tree = the model. (Not necessarily binary — can be ternary, etc.)
- **Tennis example:** past players reported whether they enjoyed playing under each condition:
  - Outlook: sunny / cloudy / rain · Rain: light / strong · Humidity: high / normal · Wind: weak / strong → outcome **Play? yes/no**.
  - New data ("it's slightly cloudy") → walk the tree → **yes/no**.
- **Target variable** = the outcome (here Boolean yes/no; can also be a **number**).

#### Regression Tree (numeric target) — **Zillow example**

- Same tree structure, but **leaves predict numbers**.
- **Zillow.com:** all US home sales are **public data** → Zillow mines them; each split = a feature (**# bedrooms, # bathrooms, sq ft, yard, school quality, crime rate, noise, hospitals…**) → predicts your home's value.
- **CART = Classification And Regression Trees** (the unified algorithm).
- **Wine example (classification tree):** scatter-plot each bottle by **alcohol % (x)** vs **color intensity** (light passing through; dense wine blocks light). Taste-label a sample as **good / questionable / cheap** → build splits like `if color intensity < 4 …`, `if alcohol < 13.8 …` → classify a new bottle.
- **Decision trees are HIGHLY TRANSPARENT** → great for **Explainability (XAI)**: you can trace exactly why the AI decided "yes," and retrain if you disagree. (Most transparent algorithm — "like marbles, you know which way it'll fall.")

### 4.2 Support Vector Machine (SVM) — Vapnik (Russian)

- Given **two labeled classes**, draw the **line that separates them with the widest possible margin** (widest "street").
- **Support vectors** = the boundary points that "hold up" the line from both sides; nudging a support shifts the line, nudging an interior point doesn't.
- That separating line/plane = the **model** → new point lands on one side → classified.
- **Binary classifier** (always A or B). In higher dimensions the line becomes a **hyperplane** (works in any number of dimensions).
- **Special case:** one support per side → just **join the two supports** and take the **perpendicular bisector** = widest separation.
- **Limitation:** the **decision boundary in 2D is always a straight line** (no kinks). If the classes are badly intermixed / not linearly separable, **SVM can't do it** → use a **neural network** (deep learning can model any boundary, however convoluted).
- **MIT lecture (Patrick Winston):** "widest street approach"; notes that great algorithms are still being discovered ("not all tricks found"), and that the SVM math is **just linear algebra**; each SVM unit is structured like a **neuron** (weights × inputs).

### 4.3 K Nearest Neighbors (KNN) — Classifier

- New point is classified by its **K nearest neighbors** (use an **odd** K to avoid ties) → **majority vote**.
- **K choice:** K=1 too few (over-dependent on one point); K=7 too much; **K=3 is a good default**.
- **Bank-loan example:** axes = **age** vs **loan amount**; past customers labeled **default (red)** vs **non-default (green)**. New applicant → find 3 nearest neighbors → mostly good = approve, mostly bad = deny. (Effectively stereotyping by similarity to past people.)
- **Lazy learner** — no model pre-built; it "learns at runtime" (computes neighbors only when a new point arrives). Still modeling, just at the last minute.
- **Normalize the data** to a **unit square** (divide each axis by its max → 0–1) so a skewed/squished axis doesn't distort **Euclidean distance**.

### 4.4 Naive Bayes — Classifier

- **"Naive"** because it assumes **Class Conditional Independence (CCI)** — the **columns are independent** of each other.
  - ✅ Good fit: **fruit properties** (color, size, weight, smell — uncorrelated) → use Naive Bayes.
  - ❌ Bad fit: **soil temperature vs humidity** (very hot soil can't be humid → correlated) → don't.
- **Reverend Thomas Bayes** — a Christian minister; his notebooks were **published only after his death** (per his wishes) → contained the whole theorem of conditional probability.
- **Bayes' rule** — write it **symmetrically** (don't divide):
  - **`P(A|B) · P(B) = P(B|A) · P(A)`**
  - (Conceptually: P(test positive | have Covid) ≠ P(have Covid | test positive) — two different things, but linked.)
- **Apple-basket example:**
  - **Prior** (past counts): 40 green vs 20 red → naively "probably green."
  - **New evidence** (look locally): nearby = **3 red, 1 green**.
  - **Posterior = Prior × Likelihood:** `(4/6 · 1/40)` for green vs `(2/6 · 3/20)` for red → green works out to `1/60`, **3× lower** than red's `1/20` → **answer flips to RED**.
- Takeaway: combine **prior belief** with **new local evidence** → updated **posterior** decision.

### 4.5 K-Means Clustering — Clustering

- **Use case:** customer **segmentation** (Amazon, Netflix). Cluster people on features (**age, income, location, education, race/name proxy, behavior**) → **target marketing** per cluster.
  - B-school name for this: **database/customer segmentation** ("database marketing").
  - Segmentation flavors: **demographic, psychographic (creepy profiles from click behavior), behavioral, geographic.**
  - **Gold / Silver / Bronze** clients (by orders/year × spend per order).
- **Centroid** of a cluster: **`(Σxᵢ / n, Σyᵢ / n)`** — the "center of mass."
- **Why you need the centroid:** a **new point** is assigned to the **nearest centroid** → that's its cluster.
- **Iterative algorithm (the magic):**
  1. **Guess K fake centroids** (random, not coincident).
  2. **Assign** every actual data point to its nearest fake centroid (temporary membership).
  3. For each fake centroid, **recompute** the centroid of its temporary members.
  4. **Move** the centroid toward that new position — but only a **small fraction** (a **learning rate**, like in neural nets), not in one jump.
  5. **Repeat** → centroids trace a curvy "particle trail" and **always converge** to the true centroids (points eventually stop moving).
- **Choosing K — the Elbow Method:** plot **error vs K**; error drops then **bends** (the "elbow"); the K at the bend = ideal cluster count. (K is an **art, not a science.**)
- **Hierarchical clustering / Dendrogram:**
  - Cluster within a cluster within a cluster → a **binary tree of clusters** (a **dendrogram**) → enables **hyper-targeted** marketing (e.g. "rich people who buy cars" vs "rich people who buy wine").
  - **Top-down** (split the whole) and **bottom-up** (merge from singletons) give the **same model** — because the model depends on where points lie in space, not where you start.

### 4.6 Embeddings (key conceptual idea)

- **One row of a table = one point in multidimensional space; each column = one axis.**
- A billion rows → a billion points. Those points have a **distribution / pattern** → that's what you mine (cluster them, draw an SVM plane, etc.).

### 4.7 A Priori / Shopping Basket Analysis — Association Mining

- Finds **what items co-occur** (bought/watched/taken together).
- **Diapers + wine example:** appears in **3 of 5** baskets → manager places them together. *(Story behind it: new parents up at 3am, change the baby, then drink half a wine bottle to fall back asleep — there's often a real reason behind an association.)*
- **Support threshold (hyperparameter):** "tell me if it happens ≥ 90% / 70% / etc." → different thresholds → different rules.
- **Direction matters (asymmetry):** **toys → batteries** ("batteries not included" → you buy batteries), but **batteries ↛ toys**. A causes B without B causing A.
- **Two filtering styles:**
  - **Collaborative filtering** = recommend based on **what other people did** (shopping-basket style).
  - **Content-based filtering** = recommend based on the **content itself** (all blues music, all ML books, all horror movies).

### 4.8 Linear Regression — Regression

- Fit a straight line: **`y = m·x + c`** (m = slope = tan θ; c = y-intercept).
- **Example:** **high-school GPA (x)** vs **college GPA (y)** → ~`0.9 · HS_GPA + 2.45`. New student's HS GPA → predict college GPA → flag students who need a (free) mentor.
- **Goal = best fit**, i.e. **minimize the error** (the gaps when points project back to the line — "error bars").
- **Bias–Variance tradeoff:**
  - **High variance / overfitting** = a wiggly curve threading every point → just **memorized** the data, learned nothing (analogy: an exam that only tests rote PowerPoint recall). **Bad.**
  - **High bias / low variance** = a line skewed toward low values, ignoring the highs. **Bad.**
  - **Ideal** = a line through the **aggregate** that captures the **overall pattern** (the "essence/gist"), not every point.
- Once fit, the line **replaces the data** for prediction.

### 4.9 Time Series Analysis

- Fit a **straight line + a superposed cyclical pattern** (combine them → wiggly trend).
- Used for **stock prices, weather, economics**.
- Classic method: **ARIMA**. Now: **LLMs** can do time-series too (time data ≈ token data) → prompt "what happens 10 years from now?"

### 4.10 Nonlinear Regression

- Data isn't a straight line → fit a curve.
- **Parabola example:** **age (x)** vs **hours of TV (y)** — high for babies & retirees, low for busy middle-aged → fit **`y = a·x² + b·x + c`**. Predict TV hours for a new person by age.
- **Multidimensional surface example (Amazon salary):** features = **years of education, years in industry** → fit a **surface** → predict a fair salary offer for a new hire.
- **Non-parametric modeling:**
  - You **don't write an explicit equation** in terms of the variables; the variables are there **implicitly**.
  - **Bézier curves / B-splines** (Adobe Illustrator pen tool): the curve is controlled by **control vertices (CVs)** — drag a CV, the curve changes — but there's **no explicit x–y equation**. Same idea applied to model data.
- **Overfitting visual:** a **lumpy surface** that bulges to hit every red point → would hand a new hire an artificially inflated salary. Want a **smooth** sheet instead.

### 4.11 Logistic Regression — actually a Classifier

- Despite the name, it's a **(usually binary) classifier**.
- The **sigmoid curve** maps any x in **(−∞, +∞)** → y in **[0, 1]**.
  - **Inflection point** at the center (y = 0.5): **curvature = 0**, where curvature flips sign (positive ↔ negative).
- Classify a new point by where it lands on y: below/above a cutoff → class A vs B (or split y into thirds for **multi-class**).
- **Bridge to neural networks** — the sigmoid here is the same nonlinearity each neuron uses.

### 4.12 Ensemble Learning (meta-algorithm)

- **Combine many classifiers** and **take a vote** (odd number → no ties). "Second opinion / crowdsourcing / many eyeballs."
- **Boosting** → combine learners' outputs.
  - **AdaBoost (Adaptive Boosting):** if one learner is consistently right and another consistently wrong, **weight the votes** (e.g. punish the bad one from 0.2 → 0.1, reward the good one) → **weighted average**.
  - **CatBoost** (from **Yandex**) — another boosting method.
- **Bagging (Bootstrap Aggregating):** partition data into many subsamples → build a **mini decision tree** on each → push new data through **all** trees → **average / vote**.
  - **Random Forest** = the classic bagging example (many trees > one giant tree).
- **XGBoost (Gradient Boosting):** modifies the trees using the **loss function / gradient descent** (the real world tells you how much to rebalance each tree).
  - **XGBoost wins the most Kaggle competitions** — *not* a neural network. "Want to win Kaggle? Learn XGBoost."

------

## PART 5 — NEURAL NETWORKS (DEEP DIVE)

### 5.1 The 3 kinds of AI

1. **Rule-based / symbolic AI** — not the focus (database-driven ML isn't this). *(Prof worked ~years on symbolic AI; that project "basically failed.")*
2. **Reinforcement learning** — give the AI a **goal**; it acts and you **reward/punish** actions (lots of robotic learning).
3. **Data-based (neural networks)** — **the focus.** Detect patterns in data → build the AI. Covers supervised, unsupervised, and **LLMs**.

### 5.2 One neuron

- Inputs `x₀, x₁, x₂…` come in (from the real world or other neurons), each multiplied by a learned **weight** `w₀, w₁, w₂…`, plus a **bias `b`**:
  - **`z = Σ(wᵢ · xᵢ) + b`** ← this alone is **multi-linear regression** (the bias `b` is just the **`c`** in `y = mx + c`; it shifts the sum positive/negative).
  - The `Σ(wᵢxᵢ)` dot product is **why GPUs** matter.
- **CRITICAL — the linchpin:** if a neuron only output the linear sum, **nothing ever converges** — no matter how many layers/epochs, the loss never drops. You **must** pass `z` through a **nonlinear activation**:
  - **Sigmoid: `1 / (1 + e^(−z))`** → now magic happens, convergence works.
  - **Analogy:** like **contrast enhancement in Photoshop** — push blacks blacker and whites whiter; the neuron "holds and fires" instead of leaking linearly.
- **Philosophical caution:** the real brain has **no numbers, no floating point, no sigmoid** — only chemical phenomena. A neural net is a **model** of the brain, not the brain. **The map is not the territory.** (Prof's pet peeve: don't claim "the brain does matrix math.")

### 5.3 Activation function history

| Function                                    | Behavior                                              | Verdict                                   |
| ------------------------------------------- | ----------------------------------------------------- | ----------------------------------------- |
| **Linear neuron** (~1960)                   | output = linear sum                                   | **Never worked**                          |
| **ADALINE** (Adaptive Linear Neuron, ~1960) | early linear neural net                               | historical                                |
| **Binary threshold**                        | output 0 below cutoff, flips to 1 above               | didn't work well                          |
| **ReLU** (rectification)                    | `y = 0` if x < 0, else `y = x` (clamp negatives to 0) | **Used in CNNs** (no negative RGB colors) |
| **Sigmoid**                                 | smooth 0→1 nonlinearity                               | **What really worked** ✅                  |

### 5.4 Training = the "exam" analogy

- Past data table: all columns except the last = **independent variables**; the **last column = the label** (e.g. loan repaid yes/no).
- Feed one row at a time → network predicts → compare to the known label → **loss** if wrong.
- Run all rows → tally errors → **"you scored 8/100, you fail."**
- This is **supervised learning** (drop the label column → unsupervised, as with LLMs / ChatGPT which just learned word associations from raw English — *insight from **Alec Radford** at OpenAI: "just feed it English and see what happens" — and it worked*).
- **Goal of training:** learn the **overall pattern**, **not memorize** row by row.
- **Pattern recognition intuition:** we recognize the **same letter across countless fonts** because we learned the **overall shape**, not a pixel-perfect template — that's what "learning a pattern" means.
- **Applications:** facial expressions, "is this mushroom safe?", cloud/bird identification, factory gauge monitoring (normal vs meltdown), shoplifter detection.

### 5.5 Backpropagation

- **Geoffrey Hinton** (one of the **3 Turing Award winners** for AI) — **1985 backprop paper**.
- **Data flows FORWARD; error-fixing flows BACKWARD.**
- Mechanics of **one epoch**:
  1. **Forward pass** → get a score.
  2. Starting at the **last layer**, nudge each weight **slightly up/down** (using the **error gradient**) so the next pass scores a bit better.
  3. Propagate the correction **layer by layer back to the first layer**.
- Repeat for **many epochs** (10,000+, can run for days) → accuracy climbs, then the **error flattens** and won't drop further (because you only need to fit the **aggregate**, not every point → stop, "as good as it gets").
- **Loss functions** (all just measure error):
  - **Parabolic / squared error:** `½ · (predicted − true)²` (squared so sign of the error doesn't matter).
  - Also **cross-entropy / log loss**, etc.
- **Alternatives to backprop:** write the whole network as a **differential equation** and solve via calculus; **stochastic gradient descent**, **conjugate gradient** (numerical step methods). Newer: **Neural ODEs / Fourier models** treat the system as a **continuous field** → more accurate than step-by-step backprop. → *backprop may not be the ultimate architecture.*

### 5.6 Scale, minima, hyperparameters

- **"10 trillion parameters" = 10 trillion weights**, each randomly initialized in **[−1, 1]**. Training (the expensive GPU part, ~$ millions) nudges each toward a good value.
  - **Global minimum** (best) vs **local minimum** (good enough, still better than the start).
- **Learning rate** (hyperparameter — metadata, *not* your data): how far to move each weight per step. Set by **trial and error / art**:
  - **Too high** → overshoots, **oscillates back and forth**, error can get **worse**.
  - **Too low** → converges but **wastes computation**, very slow.
  - **Good rate** → fast descent that settles at a low floor.
- **Momentum:** add a fraction of the **previous epoch's** update to the current one (**Nesterov momentum** = a variant).
- Different backprop algorithms reach the **same place** (same minimum) via **different weight paths**.

------

## QUICK-REFERENCE: ALGORITHMS BY THE 4 TYPES

| Type                | Algorithms in this lecture                                   |
| ------------------- | ------------------------------------------------------------ |
| **Classification**  | Decision Tree (C4.5/C5.0, CART), SVM, KNN, Naive Bayes, Logistic Regression, Neural Networks |
| **Clustering**      | K-Means, Hierarchical (Dendrogram)                           |
| **Association**     | A Priori / Shopping Basket / Association Mining (collaborative & content-based filtering) |
| **Regression**      | Linear, Nonlinear (incl. non-parametric / B-spline), Time Series, Regression Tree |
| **Meta (ensemble)** | Bagging (Random Forest), Boosting (AdaBoost, CatBoost, XGBoost) |

| Concept                       | One-liner                                                    |
| ----------------------------- | ------------------------------------------------------------ |
| **Lazy learner**              | KNN — no pre-built model; computes at runtime                |
| **Transparent / explainable** | Decision trees & clustering (you can see *why*)              |
| **Binary classifier**         | SVM, (usually) Logistic Regression                           |
| **The linchpin**              | The **sigmoid** nonlinearity — without it, neural nets never converge |
| **Elbow method**              | Pick K in K-means where the error curve bends                |
| **Posterior**                 | Prior × Likelihood (Naive Bayes)                             |
| **Overfitting**               | High variance — memorized data, learned nothing              |
| **Underfitting**              | High bias — model ignores part of the data                   |

------

## NAMES & TOOLS MENTIONED

- **People:** Leslie Valiant (BSP, 1992), Leonhard Euler (graph theory), Vladimir Vapnik (SVM), Thomas Bayes, Andrew Ng (Stanford ML / Coursera), Geoffrey Hinton (backprop, Turing Award), Patrick Winston (MIT SVM lecture), Alec Radford (OpenAI), Richard Feynman, Robert Pirsig.
- **Frameworks:** Hadoop/MapReduce, Hive, Pig, Musketeer, AWS EMR, Spark (RDD, PySpark, ex-Shark), Flink, Storm, Kafka, Samza, BSP, Pregel, Giraph, GoldenOrb/GPS, XGBoost, CatBoost.
- **AI media tools (side demo):** **Suno** (song generation — flooding Spotify with ~100k+ tracks/day), **ACE-Step / ACE Studio** (local, open-source music gen on GitHub), **Voices.AI** (real-time voice changer), **Qwen** (Alibaba LLM).



# 6/25 CS585 Lecture Notes — ML, Gen AI, Data Visualization & Data Governance

> Cheatsheet covering the data side of ML, generative AI internals, the full data-visualization tour, and the "GPS-ETC" governance framework. ⭐ = flagged by the professor as **exam-relevant**.

------

## 1. ML & Neural Network Recap

**Core idea:** Train one model (a neural network) on **past labeled data** → it learns the inherent pattern → feed it **new unseen data** → it acts/classifies correctly. *It's all about data.*

- **Canonical example — credit card binary classifier:** millions of rows of past applicants (income, age, etc.) + a known label (became good vs. bad customer). Network learns the pattern → new applicant fills form → instant accept/reject.
- **Math view:** treat label `y` as a function of input columns `x₀, x₁, x₂, …`
  - Linear part: `y = m₀x₀ + m₁x₁ + m₂x₂ + … + bias`
  - Each `m` = a slope (weight); the final constant = **bias** (the y-intercept).
  - Weights are **hardcoded numbers the neurons learned** → the function is **deterministic**.
- **Why linear isn't enough → the Sigmoid:** every neuron applies a nonlinearity
  - `σ(y) = 1 / (1 + e^(−y))`
  - This tiny tweak turns linear data into **nonlinear**, which is what makes learning possible.
  - **Without it, learning is impossible — linear neurons cannot learn at all.**
- **Labeled vs. unlabeled data:**
  - **Supervised learning** = labeled data (has the label/answer column).
  - **Unsupervised learning** = unlabeled data (e.g., all English text corpus). This is what ChatGPT is trained on. Still data — language, code, images.

------

## 2. CNN — Convolutional Neural Network

**Use case:** image recognition (cats, dogs, road objects).

**Structure:** image-processing layers **first**, then a standard neural network (**fully connected, FC**) only at the **very end**.

- **Why shrink the image?** Even with modern hardware you can't process huge images → must simplify.
- **Layer types:** convolution, **max pooling**, ReLU. Each layer shrinks the image (e.g., to ¼ size).
- **Pooling = image-size reduction:** throw away pixels in both x and y directions.
  - **Max pooling:** in each group of 4 pixels, keep the **largest** value.
  - **Min pooling:** keep the **lowest** value.
- **End result:** a big image (e.g., a zebra) becomes a **single tiny column of numbers** (RGB pixel data) → this trains the FC network → "this is what a zebra looks like." Do the same for horses, dogs, etc. → learns to classify.
- **FC layer:** every neuron connects to every neuron to its right; at this point it's pure numbers, no images.
- **Convolution kernel:** slide a small matrix over the image; each pixel becomes a multiplier, the weighted average replaces the center pixel. Slide across the whole image → blur / sharpen / edge-detect. (Classic CS image processing.)
- **Self-driving cars:** the TPU sees a **much simplified representation**, not the raw windshield image — because that's what can actually be detected.
- **Keras vs. TensorFlow:** in **Keras**, 1 layer = 1 line of Python (~8 lines for a whole CNN). Raw **TensorFlow** = 200–300+ lines for the same thing. Keras **compiles down to** TensorFlow.

------

## 3. GAN — Generative Adversarial Network ⭐ (origin of "Gen AI")

**Origin:** **Ian Goodfellow, 2014** — before any LLMs existed. This is where the "G" in **G**enerative AI comes from.

**Two networks competing:**

| Network                       | Role                                       | Direction                |
| ----------------------------- | ------------------------------------------ | ------------------------ |
| **Discriminator** ("teacher") | Classifies: real face → 1, junk → 0        | Forward (classification) |
| **Generator** ("student")     | Takes **random noise** → produces an image | Reverse (generation)     |

**Training loop:**

1. Generator turns random noise into an image → shows it to the teacher.
2. Teacher rejects it → **large error/loss**.
3. Error **backpropagates both ways**:
   - Teacher gets **tougher** (would punish the same image more next time).
   - Student adjusts its layers to make a **slightly better** image next epoch.
4. Repeat for many cycles. Eventually the student fools the teacher → **no distinction between real and fake** → **stop**.

**Result:** generator autonomously creates **photorealistic faces from pure random noise** (every pixel = random RGB). Two loss functions — one for teacher, one for generator.

- **Paper explosion:** 2014 → 1 paper (Goodfellow). After that, exponential growth — countless GAN variants, many were entire PhD theses.
- **Demo — `thispersondoesnotexist.com`:** each refresh = a brand-new fake person generated from noise. **Not stored, not stolen** — generated live. Occasional **artifacts/mistakes** appear.
- **Variants:** ThisWaifuDoesNotExist, ThisAirbnbDoesNotExist (fake listings → scam potential), fake Google Earth cities with full road/satellite data.
- **Can be trained on anything:** faces, boats, architectural/circuit diagrams, graphic design.

------

## 4. Encoder–Decoder & Variational Autoencoders (VAE)

- **Encoder:** compresses a face (or all of English) into a **smaller, compact representation** — a statistical summary, NOT a copy of all pixels.
- **Decoder:** the opposite — takes the squeezed representation and **reconstructs the full original**. Magical that it works despite "losing" so much.
- **ChatGPT / Qwen flow:** pre-train (encode all English) → give a prompt → decode → full result. (e.g., trained on C++ → prompt "write a Fibonacci generator" → working code.)

**Variational = add a probability distribution around each encoded point:**

- **Without it (point data):** music exists *only* at exact coordinates — nothing in between, no interpolation.
- **With it:** every point in the space has *some* interpolated version. Lets you blend (e.g., blues + jazz + Indian classical at once).
- **Latent space:** the vector/coordinate space where all encoded dots live; you interpolate within it.
- **Hallucination = interpolating far from real data points.** The real answers sit at specific locations; if you prompt "far away," the model still interpolates and produces something **statistically possible but not necessarily correct**.

**Definitions:**

- **"Auto"** = encoder + decoder combined in the **same architecture**.
- **"Variational"** = you can **interpolate** between things.
- **VAE** = both together. (A GAN also has both networks in one architecture.)

------

## 5. Pre-LLM Gen AI Demos (all encoder/decoder — NOT Stable Diffusion/Midjourney/LLMs)

- **QuickDraw:** millions of people draw objects (glasses, cake…) → becomes training data → teaches a network what each object looks like.
- **AutoDraw:** you sketch → it classifies → offers a **cleaned-up version** to drop into a PowerPoint.
- **Teachable Machine (Google):** train ML models in-browser, **no code**.
  - Record webcam samples → train → use in your own sites/apps.
  - The model is just a **JSON file** (network structure + weights) = an **open-weights** model.
  - Use cases: physical-therapy pose detection, trash-sorting robot, "only let my dog in" detector.
- **Open weights vs. closed:**
  - **Closed:** OpenAI, Anthropic (Claude), Gemini — want to monetize.
  - **Open weights:** Chinese models (e.g., GLM) — release the entire trained model.
- **Edge hardware:** **ESP32** microcontroller ≈ $4–5; with a camera ≈ $10. Train on a laptop → transfer model via USB-C → runs **real-time** on the chip.

------

## 6. Self-Driving / CNN for Autonomous Vehicles (2016 Nvidia/Tesla demo)

- Uses **camera data, NOT LiDAR** — raw images like a human sees through the windshield.
- **Per-frame detection, no tracking** — depth estimation, raw detections each frame.
- **Training scale:** ~7,000 images / ~33,000 unique objects.
- **Synthetic data augmentation:** crop, warp, rotate, recolor → turn 7,000 images into ~70,000.
  - "Not fooling anybody, but the network thinks it's new data." Also called **data amplification**.
- **ImageNet:** a public dataset of ~16 million **hand-labeled** images.
- **Segmentation:** cut the image into pieces, identify each piece, calculate **free space**. "Which pixel associates with which thing."
- **Parallel networks (MapReduce-like):** many networks read the **same image simultaneously** — one looks for cars, one for road, one for traffic lights, one for crosswalks/pedestrians → combined → car decides what to do.

------

## 7. AI Hardware

- **Edge TPU / Coral USB accelerator:** plug into USB → hardware acceleration for **inference**; offloads models (e.g., from Teachable Machine) and runs much faster (chips optimized for inference only).
- **OpenAI "Jalapeño" chip** *(news item from lecture, w/ Broadcom):* ~9 months from design → production. An **inference-acceleration** "intelligence processor" so OpenAI avoids paying Nvidia for GPUs. (Training is handled by a separate chip.)
- **Takeaway:** *"The world is short on compute — we need chips."*

------

## 8. Anthropic vs. Alibaba *(news item from lecture)*

- Anthropic formally **accused Alibaba** of querying Claude ~20 million times, harvesting the answers to **distill/train their own model**.
- Alibaba allegedly created **~20,000 fake accounts** (terms allow one account per company).
- Not "theft" of stored data — they submitted prompts and got answers — but violated terms via fake accounts. Anthropic reportedly asked the US government to intervene.
- **Irony noted:** AI companies themselves scraped the internet and digitized/destroyed physical books — also a form of "stealing."

------

## 9. TensorFlow Playground — Neural Network Demo ⭐ (hyperparameters)

- Tiny network: 2 layers, 2 inputs (`x1` = blue dots, `x2` = orange dots). Goal: draw the **decision boundary**.
- **Epoch** = one backpropagation pass; **Δw** = weight update. Watch the **error drop** → boundary forms → stop.
- You can **delete neurons** to test how minimal an architecture still works.
- **Hyperparameters** = settings that are **NOT part of the data** (the data is the dots).
- **Learning rate** is critical:
  - **Low (~0.03):** converges cleanly.
  - **High (~1.0):** weights bounce around, oscillate, never settle.
  - **Very high (~3):** no convergence, error blows up.
- **Gradient-descent intuition:** too-big steps **overshoot the minimum** → bounce back and forth → never reach the ideal (lowest-error) weight.

------

## 10. More Applied AI

- **Cassava disease detection (Tanzania):** phone app (TensorFlow). Photo of a leaf → classifies the disease → suggests treatment (fertilizer/pesticide). Needs labeled training data (good leaves vs. many kinds of bad leaves). Uses a **Single Shot Detector (SSD)**.
- **Data labeling / annotation industry:** drawing bounding boxes ("this is a chair") = the source of supervised data; companies make big money doing it.
  - **Alexandr Wang → Scale AI** (a data-labeling company). **Meta acquired it** and brought him in to lead — context: Yann LeCun left Meta for Paris around the same time.
- **Use Keras or PyTorch, not raw TensorFlow** — both are high-level and compile down to TensorFlow; far more productive. (PyTorch is from Facebook.)
- **YOLO demo:** in-browser detection; the model is a **~40 MB JSON file** (open-weights), uses your camera live.

------

## 11. "Voices of Reason" — AI Skeptics

- **Rodney Brooks:** built the **Roomba** (iRobot, later acquired by Amazon); MIT robotics; maintains a yearly **scorecard of what AI still can't do**.
- **Melanie Mitchell:** did her PhD with **Douglas Hofstadter**.
  - Hofstadter wrote **"Gödel, Escher, Bach: The Eternal Golden Braid"** — Pulitzer Prize; fundamentally a book about **recursion** (Bach's recursive music, Escher's recursive art, Gödel's logic).
- **Gary Marcus:** retired NYU linguist; writes that the **"AI bubble"** is fizzing out; calls it possibly the biggest stock-market bubble ever.

------

## 12. Cutting-Edge Research Directions

- **Optical neural networks (UCLA):** train a network into **passive plastic/hologram sheets**. Light passes through → classification at **zero power**; detectors on the back read the result. *Dream: zero-power token generation for data centers.*
- **GNN (Graph Neural Networks):** a network that learns the **shapes/types of graphs** (cycles, fully-connected, etc.) and classifies them by **edges and vertices**.
- **GDL (Geometric Deep Learning):** topology-based; related to GNN but not the same.
  - **"5 G's"** (alliteration): **G**rids, **G**roups, **G**raphs, **G**eodesics, **G**auges (160-page editorial).
  - **Manifold distance vs. Euclidean distance:**
    - **Euclidean** = straight line ("as the crow flies").
    - **Manifold** = distance measured **along the curved surface**. More brain-like / "more real."
    - On a manifold, a triangle's angles can be **>180°** (sphere) or **<180°** (hyperbolic space); **exactly 180°** only on a flat plane.
  - Doing embeddings/encoding this way → a much more brain-like, accurate network.
- **Neural ODE (Neural Ordinary Differential Equations):** treat the whole network as a **system of differential equations** instead of backprop.
  - Discrete layered weights = a **choppy field**; a continuous formulation is **smoother, well-behaved** → cleaner, less error, more accurate. ("No more backpropagation.")
- **Fourier PDE / fluid mechanics:**
  - **Navier–Stokes equations** (fluid pressure, velocity, temperature) — there's a **$1M prize** for an analytic solution (only numerical solutions exist).
  - Feed an LLM **past frames** → it predicts the next iterations → matches the numerical ground truth **up to a point**, then diverges. Impressive that it agrees at all.

------

## 13. Turing Award

- **2018 winners ("godfathers of deep learning"):** **Yann LeCun** (later left Meta → AMI in Paris; known for CNNs — and credited in lecture with backpropagation), **Geoffrey Hinton**, **Yoshua Bengio** (MILA lab).
- **Controversy:** **Jürgen Schmidhuber** (Swiss) — many argue he should have shared (or even solely won) the award. He maintains a page documenting his contributions/papers that overlap with the winners'. The professor calls the omission "very sad."

------

## 14. National AI Strategies

- The **US (White House), EU, India, and China** all have ~200-page AI strategy documents.
- **They all want the same things:** better healthcare, less traffic, less crime, less pollution, better education — but there's real **competition**.
- China's document includes a solid **CNN tutorial**; India's (~115 pages) explains AI/computer vision and aims for leadership; the EU's is the **"Coordinated Plan on AI"** across member states.
- **arXiv:** check **daily** for the newest papers — the bleeding edge of the field.
- **Weights & Biases (W&B):** a site that explains papers well, often with code.

------

## 15. DATA VISUALIZATION ⭐ (big section)

**Core idea:** humans are **visual**; raw number tables mean nothing → turn data into a **picture**.

- **Data viz ≠ scientific visualization.** A cell-interior illustration is *not* data viz. **Data viz = start with data → produce pictures.**
- **Libraries:** matplotlib, seaborn, ggplot, Plotly, D3.
- **Purpose:** understand → **act/decide**. (e.g., show City Hall a **blood-red daily traffic map** to justify a new freeway on-ramp.)

### Chart types

- **Pie chart:** slice size = the number (e.g., Netflix genre popularity — romance ≈ ⅓).
- **Bar chart:** bar height = value (e.g., ages at a birthday party).
- **Bubble plot:** **bubble size/radius** = value (e.g., popular supplements: vitamin C, green tea); **position doesn't matter**.
- **Tree map:** rectangle size = amount (e.g., budget spending, or biggest files on your hard drive → then delete them).

### Maps

- **Choropleth:** each map region colored by a variable's value.
  - **Classed** (discrete buckets) vs. **unclassed** (continuous).
  - Example: West Virginia **drug-overdose deaths** (south worse than north).
- **Spatial-temporal visualization:** plot path + time on **one still map** (e.g., a hurricane weakening along its trajectory). Or animate it.

### Famous historical visualizations

- **Minard's Napoleon March (1869):** often called the **best data visualization ever**. Napoleon's army into Russia and back; **line width = number of soldiers** (decimated to ~1/10–1/20). Encodes time, **temperature**, **altitude**, and direction — all by hand.
- **John Snow's Cholera Map (1854, London):** black dots = deaths → all clustered around **one water pump** → the pump was infected → shut it down → outbreak ended. One of the first cases of **evidence-driven medicine**.
- **Florence Nightingale's Rose Diagram (Crimean War):** a nurse; watercolor chart showed soldiers were dying from **infection in the hospital, not the battlefield** → got the Queen's funding to fix it. Another early evidence-based-medicine win. (She believed "God communicates through numbers.")
- **Edward Tufte:** the **"father of information visualization"** — ~5 coffee-table books of the best examples.

### Tools (more)

- **Python:** matplotlib, seaborn, Plotly.
- **JavaScript:** **D3 ("Data-Driven Documents")** — evolved from **Protovis** (Stanford).
- **Mathematica:** `ListPlot`, list point plots, 3D (free academic accounts).
- **Tableau:** data-analysis software; has an article on the best historical visualizations.
- **JMP / SAS** ("jump"): 1980s tools, still taught in business school.
- **R / Python / JavaScript** generally.

### Network / relationship visualizations

- **Network visualization:** emails, friends, social media → find the **key node** whose removal **splits the network** (terrorist boss, NSA comms tracking, "the one person who forwards every meme").
- **US trade partners:** more volume = **thicker edge**.
- **Co-author networks:** most publishing is **local** (US–Europe collaboration is sparse) → reveals gaps.
- **Tweet-language map:** plot tweet origin + language → recreates the **map of Europe** with no drawn borders.
- **Science-field connections:** find **unconnected fields** = an opportunity to bridge them (biophysics, biochemistry).
- **Friend/enemy matrix:** red = enemies, green = friends, yellow = neutral → don't fund both sides of a conflict (e.g., Kurds + Iraq) → saves billions.
- **Media-bias chart:** Drudge Report = far right; far left equally extreme; AP/Bloomberg/BBC/Forbes/WaPo = center → aim for neutral.
- **Daily routine of famous people:** **no shared pattern** → be creative, be your own person.

### Live / real-time visualizations

- **Wind map** (live US wind velocity). **Santa Ana winds** (December) reverse direction → fuel **wildfires**.
- **Kaspersky / Malwarebytes cyber-attack maps:** live attacks between countries, backed by real incident data.
- **Earthquake maps:** a **line of quakes over weeks** → a fault about to rupture → evacuate. (Prediction is hard, but data shows where the crust is opening.)
- **Radio Garden:** streaming radio stations on a globe — pick any location.
- **Real-time stocks.**
- **Real-time world population:** births outpace deaths (~net +1000s/day). **Negative growth** now in China/Japan/Korea for the first time.
- **Kobe Bryant shot chart (LA Times poster, made in R):** **all ~30,700 career shots** — "the arc of his career."

### Spatial-temporal extras

- **Hurricane viewer:** search like a **SQL query** (e.g., "Katrina 2005").
  - **Hurricane Katrina:** Cat 5 → landfall as Cat 3 → **levees failed** → New Orleans (below sea level, "like a bathtub") flooded → ~1,800 dead, ~1,800 homeless.
- **NOAA:** all hurricanes ever on **one map** (hover for each one's history).
- **COVID slope chart:** rate up/down per state over time (March 12, 2020 = USC shut down).

### Data journalism

- Journalism **backed by data + storytelling** (data science + writing).
- Sometimes you need the **story behind the data**, not just the line.
- **VR data journalism:** immersive 3D recreation puts the viewer **inside the scene** (flood, bombing). USC has a course on it.

### Key principle ⭐: **FORM FOLLOWS FUNCTION** (alliteration)

- The **communication** aspect (do people understand?) matters **more than aesthetics** (colors, fonts).
- Do good **information communication first**, then fix the design — not the other way around.
- Side notes: **"Terrible Maps"** subreddit (funny but often true); **Atlas of Knowledge** (science + art of perception); USC course **CSCI/DSCI 554** is entirely about visualization.
- **Multivariate** = many variables on one diagram.
- ⚠️ Caveat: as humans handle less data themselves (agents don't need to "see"), visualization may become partly moot.

------

## 16. DATA GOVERNANCE — "GPS-ETC" ⭐

**Mnemonic: G-P-S-E-T-C** (all about data)

- **G** = Governance
- **P** = Privacy
- **S** = Security
- **E** = Ethics
- **T** = Trust
- **C** = Compliance

> Professor's prediction: **governance jobs will explode because of LLMs** — auditing what tokens are doing, complying with regulations.

### Privacy

- **1970s US government principles** (originally banks + federal/IRS):
  - **Openness / disclosure** — tell customers what data you collect.
  - **Secondary usage** — what else the data can be used for.
  - **Correctability** — you can fix incorrect data (a bad credit report blocks apartments/loans).
  - **Security** — keep data safe from hackers.
- **Tracking everywhere:** cookies; the USC health center can sell **de-identified** blood/urine data (it legally belongs to SC, not you).
- **China:** facial recognition everywhere → **no expectation of privacy** (good and bad uses).
- **Japan:** AI cameras flag "suspicious" behavior → **shoplifter prediction** from past data (e.g., "Vaak"); ~4% suspicion threshold.
- **US public space:** **no privacy** — anyone can photo/video you; you can be tracked across cameras and identified (Manhattan has hundreds).
- **Google tracking demo (Fox):** 2 phones (one in airplane mode, both with no SIM/WiFi).
  - On reconnect: **100+ locations, 130 activities, 152 barometric readings, ~300 KB sent to Google.**
  - **"Surveillance capitalism"** — collect data → sell **targeted ads** (Google AdWords).
  - The **airplane-mode phone logged even more** locations.
  - You can build a packet sniffer / "man-in-the-middle" with an **ESP32 (~$10)**.
- **Privacy = a LEGAL matter** (you have a right to privacy for certain data: medical, etc.).

### Security

- **A TECHNICAL matter:** passwords, firewalls, network monitoring.
- **DataBreachToday.com:** daily breaches (LastPass, Lemonade, GitHub, billions of records).
- **Hackers aren't magical** — they exploit **weak/bad security practices**. Good security → ~zero breaches.
- **Can be technically prevented.**

### Ethics

- The **uneasy gray area** — legal but feels wrong: *should we do it just because we can?*
- **Rogue AI:** superintelligence/AGI — professor thinks human-level AGI is **BS / won't happen**. Scarier and real: **robot soldiers** (e.g., North Korea) — shoot to kill, zero feelings, perfectly accurate (human soldiers might show mercy).
- **Deepfakes / fake videos:**
  - **Jordan Peele's Obama deepfake (2018)** — one of the first; a warning about fake news.
  - **Fake Abraham Lincoln** — we know it's fake only because we have real photos; **future kids won't be able to tell**.
- **Slaughterbots** (autonomousweapons.org): **swarm drones** with facial recognition + **~3 g shaped explosive** to penetrate the skull.
  - **Swarm robotics:** the whole swarm acts as one unit (like killer bees — can't destroy all of them).
  - Drones already changed the **Ukraine war**. Scientists petition to ban them by law (may be too late).
- **Bias / hidden bias.**

### Trust

- How much can you trust a company with your data if they **leak** it?
- Stores save your **card number + CVV in plain text** on public servers → hackers drain the card (often **waiting years** before using it).
- **Once trust is lost, it's never regained** (Target, Home Depot breaches).

### Compliance

- **Legal frameworks.**
- **GDPR (General Data Protection Regulation)** — EU, enforced by all member nations.
  - Fines up to **~$1M/day** (e.g., against Facebook). Ireland/France sue US companies (Apple, Microsoft).
  - Same as the 1970s US principles, **plus**:
  - **Right to be forgotten / erasure** — tell Google to delete all your search history; they must comply within ~1 day.
  - Disclosure, consent, permission for secondary usage.
- **US has no equivalent federal law** — a **patchwork by state** (deepfake porn illegal in CA, legal in TX). *Should* adopt GDPR federally, but unlikely.
- **Governance example:** a hospital sends patient data to Anthropic → Anthropic must do **governance** (e.g., never train new models on your medical data).

### Governance (the "G" — a big career)

- **Audit what the tokens are doing.**
- **Amazon Bedrock** = a model-deployment environment. The LLM/agents are just the **tip of the iceberg**; underneath sit **governance, compliance, explainability, transparency** — the bigger, harder, more important part.

### Curation

- Like a **museum curator** with limited wall space → highlight the important data.
- A big company's curation team unearths important data from raw data and makes it **reusable internally** → prevents reinventing the wheel (a new biochemist redeveloping an already-patented drug).

### Provenance & Lineage

- **Provenance:** where the data **started** (a COVID virus sequence must come from a real lab, not a faker).
- **Lineage:** where the data **traveled** (someone could poison good data and re-upload it to GitHub).
- Track **both** → trustworthy only if nobody corrupted it along the way.
- **Blockchain** fits here well: encode/encrypt a block each time data changes hands → **verifiable, immutable, undeletable**.

### Master Data Management (MDM)

- Inconsistency comes from **too many copies**.
- Fix: keep **one master copy**; everyone else points to it (read-only pointers).
- Easy, not very technical, real jobs (sometimes needs SQL).

> **Governance + Security + Privacy form a triangle** — all important.

------

## 17. GEN AI DEEP DIVE ⭐ ("there will definitely be a question")

- **Traditional ML:** table of data → NN → classify new data.
- **Reverse the direction → GENERATE.**
- **GAN = origin of the "G" in Gen AI.** Before GANs, NNs could only **classify** (Shazam: "that's blues"). Now: "make me **8 bars of blues**."
- **Style transfer (neural style transfer):** apply Van Gogh's style to **every frame** of a movie. (First neural-style-transfer paper.)

### Transformers

- **Encoder/decoder architecture** with **latent space** in the middle: encode all English → store → prompt → decode → new tokens.
- **Deployed transformers (GPT, etc.) are DECODER-ONLY** — the encoder is the pre-training part (already done), so only half is needed. (The original paper has both.)
- **Encoding (training):** given many words, learn the **most likely next word**.
- **ATTENTION:** for any word, **which other word matters most?**
  - Every word computes an attention score with **every other word**.
  - **N words → N² calculation** → this is what slows things down.
- **Context window** = how many words/tokens the prompt can hold.
  - **N² complexity limits context size.**
  - **Context** = extra inputs to the LLM (e.g., "here's similar code in Swift, now write it in Java").
- **Hyena:** a **sub-quadratic** transformer — **O(N log N)** instead of **O(N²)** → bigger context window, longer prompts.
- **Frontier models:** ~**1 million-token** context (can fit a whole book).

### Learning transformers

- **Andrej Karpathy:** ~30-min intro talk on LLMs (a household name in AI).
  - LLMs learn the **most common completions** ("cat sat on a mat / windowsill / lap") and pick the most probable.
- **TEMPERATURE:**
  - **0** = always the most probable word → **no hallucination**.
  - **Higher** = allows less-probable words → **more creativity**.
- **llm.c (Karpathy):** two simple C programs, standard gcc, **no libraries / no NumPy**.
  - `train_gpt2.c` and `test_gpt2.c`.
  - Implements the transformer math: **Keys, Queries, Values (K/Q/V)** — Queries = your prompt; Keys + Values together = the result.
  - **Training is more complex than testing.** Map the **transformer paper** to this code to learn it permanently.

### Fine-tuning

- Add domain knowledge (law, finance, medicine, crime, education).
- **Old way:** modify **all** layers/neurons.
- **LoRA (Low-Rank Adaptation, Microsoft):** don't touch the lower layers, only modify the **upper** layers. Ships as a small **separate downloadable file** (e.g., "download this → better at C++").

### RAG (Retrieval-Augmented Generation)

- LLM alone isn't enough for complex domain questions.
- **Vector RAG:** build a **vector database** of sentences (e.g., all Swift books) → LLM retrieves the answer.
- **Graph RAG:** build a **knowledge graph** → retrieve from it.
- **Hybrid RAG:** combine both.
- Can also call: Google search, database login, math function, REST API → combine answers.
- **RAG = do almost anything EXCEPT touch the actual LLM.**

### Code generation

- A huge list of tools, all serving one purpose: **generate something** — code, video, 3D graphics, music, graphic design, architecture, chip design, poetry.

### Hardware (Gen AI)

- **Hyena** (non-standard transformer) + hardware approaches.
- **OpenAI Jalapeño** (Broadcom) for fast inference.
- **Nvidia:** **Nemotron** (the LLM) on Nvidia cloud + **NIM (NVIDIA Inference Microservices)** = a REST API.
  - Upload a video → ask questions; token generation runs **on the server**.
  - *"Learn NIM microservices → get jobs."*
- **MCC** = microservices, cloud, containers.

### Small Language Models (SLM)

- Instead of going bigger (Claude ≈ 10 trillion params), what if **2 billion params = 80% as good?**
- **Gemma (Google):** ~26 billion params — a small language model.
- **Quantization:** weights stored not as 16 bits but **1.58 bits**.
  - 1 bit = 2 values; 2 bits = 4 values; **3 values needs log₂(3) ≈ 1.58 bits**.
  - 1.58-bit weights = **3 possibilities: −1, 0, +1**.
  - **BitNet (Microsoft)** / "1-bit" (1.58-bit) models on **Hugging Face** — tiny, easy to download, almost as good as big models.

### Other directions

- **World models / physical AI:** watch videos, understand physics (drop paper → it falls).
- **Embodied AI:** put the LLM on a **robot**, first-person POV.
- **Custom-purpose LLMs** (Nemotron for graphics/digital twins, animation).
- **Instrumentation:** the LLM is the tip; the base is observability + governance.
- **Synthetic data:** 7,000 frames → 70,000.
- **Diffusion models:**
  - Take a good image → **progressively add noise** → fully noisy.
  - Train on **(degraded → good)** pairs.
  - Generate: give **pure noise + prompt** ("Kung Fu Panda on the beach") → **denoise into the image**.
  - This is how **Stable Diffusion** works. Text generation can also be done this way.
- **Reasoning models → agents.**

### Agents

- An **agent = a big LOOP** with the LLM inside.
- The loop = **Reason + Act**: decide what to do → go do it (using **tools**) → repeat until finished → return the answer.
- The pattern is called the **Reason-Act loop**.

------

## 18. Miscellaneous (1 slide)

- **Efficient-write data structures:**
  - **LSM tree (Log-Structured Merge tree)** + **SSTable (Sorted String Table)** — for write-heavy, rarely-modified data; an alternative to **B-tree** indexing.
- **Data formats:** **Parquet**, **Iceberg**.
- **Lakehouse:** **data lake** (dump all data) + **warehouse**; **Hudi**, **Iceberg** ("Ice House").
- **Google Earth** = spatial data (your homework used real Google data).

------

## 📌 Exam Notes

- **Focus areas:** **spatial data**; **data mining** (less); **Gen AI** — **definitely a question**, but nothing beyond lecture (you do **NOT** need the transformer paper).
- Covers **second-half topics** (professor said he'll post a list / story).
- A **last homework** and a **sample exam** are coming — both described as **easy**.
- Mental model: the course is a **subway map of data** — get off at any stop and learn what's there.