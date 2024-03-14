The inputs (Btor2 circuits) to the algorithm selector (ML model) can be found in <https://gitlab.com/sosy-lab/research/data/word-level-hwmc-benchmarks/-/tree/main/bv/btor2>.

The labels for training can be extracted the files in <https://www.cip.ifi.lmu.de/~chien/benchexec-results/btor2c-eval/final-full-results/>.
Download <tool_name>-lazyMod.*.results.*.bv-64.xml.bz2 files from the above link, where tool_name are "cpachechecker", "esbmc", and "veriabs",

decompress them, and process the xml files.
Look for the following "run" entries in the xml file:

  <run name="../benchmarks/bv/goel-industry/cal139.yml" files="[../benchmarks/bv/goel-industry/cal139.c]" properties="unreach-call" propertyFile="../benchmarks/properties/unreach-call.prp" expectedVerdict="true">
    <column title="cputime" value="63.970950045s"/>
    <column title="memory" value="14999998464B"/>
    <column title="status" value="OUT OF MEMORY"/>
    <column title="walltime" value="63.1396222540061s"/>
    ...
  </run>
The "status" column shows the verification result of the verifier ("tool_name") on the task ("run name").

TRUE/FALSE means that the Btor2 circuit is deemed safe/unsafe by the verifier,

and the others indicate that the verifier could not solve the task due to timeout, OOM, or some error/exception.
From the status and cputime/memory columns, one could infer the most suitable verifier for each task,

which represents the label of the task in the dataset.

Once the inputs and labels are obtained, ML models can be trained.

In short, the preliminary tasks are:
- Extract labels and construct the dataset (to assess the data-processing skill)
- Train a model on the dataset (to assess the ML skill)