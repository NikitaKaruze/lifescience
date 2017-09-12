Selection Language
==================

Miew allows to view different molecule parts (subsets of atoms) using
specific visualizations. To select these subsets one should use a
*Selection Language*; its syntax is described below.

Quick Examples
--------------

-  ``chain A and not hetatm`` |br|
   select all atoms in chain A except for HETATM PDB records.

-  ``residue ALA`` |br|
   select all residues named ``ALA`` (alanine).

-  ``serial 1:10, 20:30 and type C, N`` |br|
   select Carbon and Nitrogen atoms with atom indices in range 1 through
   10 or 20 through 30 inclusively.

.. |br| raw:: html

    <br/>

Syntax
------

An *Expression* in Miew selection language consists of a *Selector* or a
set of *Expressions* joined with logical operations ``AND``, ``OR``,
``NOT`` and brackets for grouping.

::

    Expression ::=
      Selector |
      Expression 'AND' Expression |
      Expression 'OR' Expression |
      'NOT' Expression |
      '(' Expression ')'

*Selector* consists of a keyword followed by an optional comma separated
parameter list. Some keywords accept integer parameters (e.g. atom or
residue indices), others accept strings (e.g. atom or residue names).
Keywords are **case insensitive**.

Integer parameter can be a single value or range of values, where range
borders are delimited by a colon. Example: ``3:7`` defines an integer
range: 3, 4, 5, 6, and 7).

String parameters should be flanked by quotation marks unless the string
consists of letters, digits and underscores only.

::

    Selector ::=
      Keyword |
      Keyword IntegerList |
      Keyword StringList

    IntegerList ::= Range | IntegerList ',' Range
    Range ::= Number | Number ':' Number

    StringList ::= String | StringList ',' String
    String ::= AlphaNumericString | QuotedString

Keywords list
-------------

+-------------------+----------------------------------------+-------------------------------+
|Keyword            |Description                             |Example                        |
+===================+========================================+===============================+
|**all**            |all atoms                               |``all``                        |
+-------------------+----------------------------------------+-------------------------------+
|**none**           |empty subset                            |``none``                       |
+-------------------+----------------------------------------+-------------------------------+
|**hetatm**         |atoms defined as HETATM in PDB-file     |``not hetatm``                 |
+-------------------+----------------------------------------+-------------------------------+
|**water**          |water residues (WAT, HOH, H2O)          |``hetatm and not water``       |
+-------------------+----------------------------------------+-------------------------------+
|**serial** *int*   |atoms by serial numbers                 |``serial 1:10, 13, 25:37``     |
+-------------------+----------------------------------------+-------------------------------+
|**name** *str*     |atoms by names                          |``name CA, CB``                |
+-------------------+----------------------------------------+-------------------------------+
|**elem** *str*     |atoms by chemical elements              |``elem O, N, H``               |
+-------------------+----------------------------------------+-------------------------------+
|**polarh**         |polar hydrogens                         |``polarh``                     |
+-------------------+----------------------------------------+-------------------------------+
|**nonpolarh**      |non-polar hydrogens                     |``not nonpolarh``              |
+-------------------+----------------------------------------+-------------------------------+
|**altloc** *str*   |atoms by alternative location           |``altloc " ", A``              |
|                   |(conformation)                          |                               |
+-------------------+----------------------------------------+-------------------------------+
|**residue** *str*  |residues by names                       |``residue ALA, CYS``           |
+-------------------+----------------------------------------+-------------------------------+
|**sequence** *int* |residues by indices in a sequence       |``sequence 35:37``             |
+-------------------+----------------------------------------+-------------------------------+
|**residx** *int*   |residues by ordinal index               |``residx 1327``                |
+-------------------+----------------------------------------+-------------------------------+
|**icode** *str*    |residues by insertion code              |``sequence 409 and icode B``   |
+-------------------+----------------------------------------+-------------------------------+
|**protein**        |one of 22 common amino acid residues    |                               |
+-------------------+----------------------------------------+-------------------------------+
|**basic**          |basic amino acid residue: ARG, HIS, LYS |                               |
+-------------------+----------------------------------------+-------------------------------+
|**acidic**         |acidic amino acid residue: ASP, GLU     |                               |
+-------------------+----------------------------------------+-------------------------------+
|**charged**        |basic or acidic residue                 |                               |
+-------------------+----------------------------------------+-------------------------------+
|**polar**          |polar amino acid residue: ASN, CYS,     |                               |
|                   |GLN, SER, THR, TYR                      |                               |
+-------------------+----------------------------------------+-------------------------------+
|**nonpolar**       |non-polar amino acid residue: ALA, ILE, |                               |
|                   |LEU, MET, PHE, PRO, TRP, VAL            |                               |
+-------------------+----------------------------------------+-------------------------------+
|**aromatic**       |aromatic amino acid residue: PHE, TRP,  |                               |
|                   |TYR                                     |                               |
+-------------------+----------------------------------------+-------------------------------+
|**nucleic**        |nucleic residue                         |                               |
+-------------------+----------------------------------------+-------------------------------+
|**purine**         |purine nucleic residue: A, G, I and     |                               |
|                   |variations                              |                               |
+-------------------+----------------------------------------+-------------------------------+
|**pyrimidine**     |pyrimidine nucleic residue: C, T, U     |                               |
|                   |and variations                          |                               |
+-------------------+----------------------------------------+-------------------------------+
|**chain** *str*    |chain by name                           |``chain A, C, E``              |
+-------------------+----------------------------------------+-------------------------------+

