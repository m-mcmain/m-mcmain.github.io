---
layout: single
sitemap: false
permalink: /pages/Econ_390_SP26_L11_teaching/
---

[Download Jupyter Notebook Empty](https://m-mcmain.github.io/files/Econ390SP26/Lectures/Lecture11_PandasReadandWrite_empty.ipynb)

Download Jupyter Notebook Completed

# Econ 390 - Lecture 11: Pandas Read and Write
Today we will be learning how to use Pandas to read and write data files. This follows from [McKinney](https://wesmckinney.com/book/accessing-data) and [Turell](https://aeturrell.github.io/coding-for-economists/data-read-and-write.html).


## CSV Files


```python
# Read in a CSV file
macro_data = pd.read_csv('macro_data.csv')
```


    ---------------------------------------------------------------------------

    NameError                                 Traceback (most recent call last)

    Cell In[1], line 2
          1 # Read in a CSV file
    ----> 2 macro_data = pd.read_csv('macro_data.csv')
    

    NameError: name 'pd' is not defined



```python
# Don't forget!
import pandas as pd
```


```python
# Now we can read it in?
macro_data = pd.read_csv('macro_data.csv')
macro_data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_date</th>
      <th>GDP_PC1</th>
      <th>CPIAUCSL_PC1</th>
      <th>CES0500000003_PC1</th>
      <th>NASDAQCOM_PC1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01-01</td>
      <td>3.90093</td>
      <td>0.12114</td>
      <td>2.25887</td>
      <td>13.03855</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-01</td>
      <td>2.78707</td>
      <td>1.26736</td>
      <td>2.56214</td>
      <td>0.85409</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-01-01</td>
      <td>4.29244</td>
      <td>2.13144</td>
      <td>2.55661</td>
      <td>25.01118</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-01</td>
      <td>5.32535</td>
      <td>2.43900</td>
      <td>3.01869</td>
      <td>19.09546</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-01-01</td>
      <td>4.27694</td>
      <td>1.81326</td>
      <td>3.29920</td>
      <td>6.92507</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2020-01-01</td>
      <td>-0.76462</td>
      <td>1.25294</td>
      <td>4.87856</td>
      <td>28.47922</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2021-01-01</td>
      <td>10.99571</td>
      <td>4.67912</td>
      <td>4.28267</td>
      <td>40.87765</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2022-01-01</td>
      <td>9.81625</td>
      <td>7.99264</td>
      <td>5.37775</td>
      <td>-14.89260</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2023-01-01</td>
      <td>6.74315</td>
      <td>4.12772</td>
      <td>4.44473</td>
      <td>6.04126</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2024-01-01</td>
      <td>5.34489</td>
      <td>2.95161</td>
      <td>4.03304</td>
      <td>32.97673</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2025-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.90245</td>
    </tr>
  </tbody>
</table>
</div>




```python
# What does it become?
print(type(macro_data))
```

    <class 'pandas.core.frame.DataFrame'>
    


```python
# Check out the first three
macro_data.head(3)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_date</th>
      <th>GDP_PC1</th>
      <th>CPIAUCSL_PC1</th>
      <th>CES0500000003_PC1</th>
      <th>NASDAQCOM_PC1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01-01</td>
      <td>3.90093</td>
      <td>0.12114</td>
      <td>2.25887</td>
      <td>13.03855</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-01</td>
      <td>2.78707</td>
      <td>1.26736</td>
      <td>2.56214</td>
      <td>0.85409</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-01-01</td>
      <td>4.29244</td>
      <td>2.13144</td>
      <td>2.55661</td>
      <td>25.01118</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Check out the last 5
macro_data.tail()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_date</th>
      <th>GDP_PC1</th>
      <th>CPIAUCSL_PC1</th>
      <th>CES0500000003_PC1</th>
      <th>NASDAQCOM_PC1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>2021-01-01</td>
      <td>10.99571</td>
      <td>4.67912</td>
      <td>4.28267</td>
      <td>40.87765</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2022-01-01</td>
      <td>9.81625</td>
      <td>7.99264</td>
      <td>5.37775</td>
      <td>-14.89260</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2023-01-01</td>
      <td>6.74315</td>
      <td>4.12772</td>
      <td>4.44473</td>
      <td>6.04126</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2024-01-01</td>
      <td>5.34489</td>
      <td>2.95161</td>
      <td>4.03304</td>
      <td>32.97673</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2025-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.90245</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Change the index
macro_data_new_index = macro_data.set_index('observation_date')
macro_data_new_index
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GDP_PC1</th>
      <th>CPIAUCSL_PC1</th>
      <th>CES0500000003_PC1</th>
      <th>NASDAQCOM_PC1</th>
    </tr>
    <tr>
      <th>observation_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-01-01</th>
      <td>3.90093</td>
      <td>0.12114</td>
      <td>2.25887</td>
      <td>13.03855</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>2.78707</td>
      <td>1.26736</td>
      <td>2.56214</td>
      <td>0.85409</td>
    </tr>
    <tr>
      <th>2017-01-01</th>
      <td>4.29244</td>
      <td>2.13144</td>
      <td>2.55661</td>
      <td>25.01118</td>
    </tr>
    <tr>
      <th>2018-01-01</th>
      <td>5.32535</td>
      <td>2.43900</td>
      <td>3.01869</td>
      <td>19.09546</td>
    </tr>
    <tr>
      <th>2019-01-01</th>
      <td>4.27694</td>
      <td>1.81326</td>
      <td>3.29920</td>
      <td>6.92507</td>
    </tr>
    <tr>
      <th>2020-01-01</th>
      <td>-0.76462</td>
      <td>1.25294</td>
      <td>4.87856</td>
      <td>28.47922</td>
    </tr>
    <tr>
      <th>2021-01-01</th>
      <td>10.99571</td>
      <td>4.67912</td>
      <td>4.28267</td>
      <td>40.87765</td>
    </tr>
    <tr>
      <th>2022-01-01</th>
      <td>9.81625</td>
      <td>7.99264</td>
      <td>5.37775</td>
      <td>-14.89260</td>
    </tr>
    <tr>
      <th>2023-01-01</th>
      <td>6.74315</td>
      <td>4.12772</td>
      <td>4.44473</td>
      <td>6.04126</td>
    </tr>
    <tr>
      <th>2024-01-01</th>
      <td>5.34489</td>
      <td>2.95161</td>
      <td>4.03304</td>
      <td>32.97673</td>
    </tr>
    <tr>
      <th>2025-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.90245</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Introspection
pd.read_csv?
```


    [31mSignature:[39m
    pd.read_csv(
        filepath_or_buffer: [33m'FilePath | ReadCsvBuffer[bytes] | ReadCsvBuffer[str]'[39m,
        *,
        sep: [33m'str | None | lib.NoDefault'[39m = <no_default>,
        delimiter: [33m'str | None | lib.NoDefault'[39m = [38;5;28;01mNone[39;00m,
        header: [33m"int | Sequence[int] | None | Literal['infer']"[39m = [33m'infer'[39m,
        names: [33m'Sequence[Hashable] | None | lib.NoDefault'[39m = <no_default>,
        index_col: [33m'IndexLabel | Literal[False] | None'[39m = [38;5;28;01mNone[39;00m,
        usecols: [33m'UsecolsArgType'[39m = [38;5;28;01mNone[39;00m,
        dtype: [33m'DtypeArg | None'[39m = [38;5;28;01mNone[39;00m,
        engine: [33m'CSVEngine | None'[39m = [38;5;28;01mNone[39;00m,
        converters: [33m'Mapping[Hashable, Callable] | None'[39m = [38;5;28;01mNone[39;00m,
        true_values: [33m'list | None'[39m = [38;5;28;01mNone[39;00m,
        false_values: [33m'list | None'[39m = [38;5;28;01mNone[39;00m,
        skipinitialspace: [33m'bool'[39m = [38;5;28;01mFalse[39;00m,
        skiprows: [33m'list[int] | int | Callable[[Hashable], bool] | None'[39m = [38;5;28;01mNone[39;00m,
        skipfooter: [33m'int'[39m = [32m0[39m,
        nrows: [33m'int | None'[39m = [38;5;28;01mNone[39;00m,
        na_values: [33m'Hashable | Iterable[Hashable] | Mapping[Hashable, Iterable[Hashable]] | None'[39m = [38;5;28;01mNone[39;00m,
        keep_default_na: [33m'bool'[39m = [38;5;28;01mTrue[39;00m,
        na_filter: [33m'bool'[39m = [38;5;28;01mTrue[39;00m,
        verbose: [33m'bool | lib.NoDefault'[39m = <no_default>,
        skip_blank_lines: [33m'bool'[39m = [38;5;28;01mTrue[39;00m,
        parse_dates: [33m'bool | Sequence[Hashable] | None'[39m = [38;5;28;01mNone[39;00m,
        infer_datetime_format: [33m'bool | lib.NoDefault'[39m = <no_default>,
        keep_date_col: [33m'bool | lib.NoDefault'[39m = <no_default>,
        date_parser: [33m'Callable | lib.NoDefault'[39m = <no_default>,
        date_format: [33m'str | dict[Hashable, str] | None'[39m = [38;5;28;01mNone[39;00m,
        dayfirst: [33m'bool'[39m = [38;5;28;01mFalse[39;00m,
        cache_dates: [33m'bool'[39m = [38;5;28;01mTrue[39;00m,
        iterator: [33m'bool'[39m = [38;5;28;01mFalse[39;00m,
        chunksize: [33m'int | None'[39m = [38;5;28;01mNone[39;00m,
        compression: [33m'CompressionOptions'[39m = [33m'infer'[39m,
        thousands: [33m'str | None'[39m = [38;5;28;01mNone[39;00m,
        decimal: [33m'str'[39m = [33m'.'[39m,
        lineterminator: [33m'str | None'[39m = [38;5;28;01mNone[39;00m,
        quotechar: [33m'str'[39m = [33m'"'[39m,
        quoting: [33m'int'[39m = [32m0[39m,
        doublequote: [33m'bool'[39m = [38;5;28;01mTrue[39;00m,
        escapechar: [33m'str | None'[39m = [38;5;28;01mNone[39;00m,
        comment: [33m'str | None'[39m = [38;5;28;01mNone[39;00m,
        encoding: [33m'str | None'[39m = [38;5;28;01mNone[39;00m,
        encoding_errors: [33m'str | None'[39m = [33m'strict'[39m,
        dialect: [33m'str | csv.Dialect | None'[39m = [38;5;28;01mNone[39;00m,
        on_bad_lines: [33m'str'[39m = [33m'error'[39m,
        delim_whitespace: [33m'bool | lib.NoDefault'[39m = <no_default>,
        low_memory: [33m'bool'[39m = [38;5;28;01mTrue[39;00m,
        memory_map: [33m'bool'[39m = [38;5;28;01mFalse[39;00m,
        float_precision: [33m"Literal['high', 'legacy'] | None"[39m = [38;5;28;01mNone[39;00m,
        storage_options: [33m'StorageOptions | None'[39m = [38;5;28;01mNone[39;00m,
        dtype_backend: [33m'DtypeBackend | lib.NoDefault'[39m = <no_default>,
    ) -> [33m'DataFrame | TextFileReader'[39m
    [31mDocstring:[39m
    Read a comma-separated values (csv) file into DataFrame.
    
    Also supports optionally iterating or breaking of the file
    into chunks.
    
    Additional help can be found in the online docs for
    `IO Tools <https://pandas.pydata.org/pandas-docs/stable/user_guide/io.html>`_.
    
    Parameters
    ----------
    filepath_or_buffer : str, path object or file-like object
        Any valid string path is acceptable. The string could be a URL. Valid
        URL schemes include http, ftp, s3, gs, and file. For file URLs, a host is
        expected. A local file could be: file://localhost/path/to/table.csv.
    
        If you want to pass in a path object, pandas accepts any ``os.PathLike``.
    
        By file-like object, we refer to objects with a ``read()`` method, such as
        a file handle (e.g. via builtin ``open`` function) or ``StringIO``.
    sep : str, default ','
        Character or regex pattern to treat as the delimiter. If ``sep=None``, the
        C engine cannot automatically detect
        the separator, but the Python parsing engine can, meaning the latter will
        be used and automatically detect the separator from only the first valid
        row of the file by Python's builtin sniffer tool, ``csv.Sniffer``.
        In addition, separators longer than 1 character and different from
        ``'\s+'`` will be interpreted as regular expressions and will also force
        the use of the Python parsing engine. Note that regex delimiters are prone
        to ignoring quoted data. Regex example: ``'\r\t'``.
    delimiter : str, optional
        Alias for ``sep``.
    header : int, Sequence of int, 'infer' or None, default 'infer'
        Row number(s) containing column labels and marking the start of the
        data (zero-indexed). Default behavior is to infer the column names: if no ``names``
        are passed the behavior is identical to ``header=0`` and column
        names are inferred from the first line of the file, if column
        names are passed explicitly to ``names`` then the behavior is identical to
        ``header=None``. Explicitly pass ``header=0`` to be able to
        replace existing names. The header can be a list of integers that
        specify row locations for a :class:`~pandas.MultiIndex` on the columns
        e.g. ``[0, 1, 3]``. Intervening rows that are not specified will be
        skipped (e.g. 2 in this example is skipped). Note that this
        parameter ignores commented lines and empty lines if
        ``skip_blank_lines=True``, so ``header=0`` denotes the first line of
        data rather than the first line of the file.
    names : Sequence of Hashable, optional
        Sequence of column labels to apply. If the file contains a header row,
        then you should explicitly pass ``header=0`` to override the column names.
        Duplicates in this list are not allowed.
    index_col : Hashable, Sequence of Hashable or False, optional
      Column(s) to use as row label(s), denoted either by column labels or column
      indices.  If a sequence of labels or indices is given, :class:`~pandas.MultiIndex`
      will be formed for the row labels.
    
      Note: ``index_col=False`` can be used to force pandas to *not* use the first
      column as the index, e.g., when you have a malformed file with delimiters at
      the end of each line.
    usecols : Sequence of Hashable or Callable, optional
        Subset of columns to select, denoted either by column labels or column indices.
        If list-like, all elements must either
        be positional (i.e. integer indices into the document columns) or strings
        that correspond to column names provided either by the user in ``names`` or
        inferred from the document header row(s). If ``names`` are given, the document
        header row(s) are not taken into account. For example, a valid list-like
        ``usecols`` parameter would be ``[0, 1, 2]`` or ``['foo', 'bar', 'baz']``.
        Element order is ignored, so ``usecols=[0, 1]`` is the same as ``[1, 0]``.
        To instantiate a :class:`~pandas.DataFrame` from ``data`` with element order
        preserved use ``pd.read_csv(data, usecols=['foo', 'bar'])[['foo', 'bar']]``
        for columns in ``['foo', 'bar']`` order or
        ``pd.read_csv(data, usecols=['foo', 'bar'])[['bar', 'foo']]``
        for ``['bar', 'foo']`` order.
    
        If callable, the callable function will be evaluated against the column
        names, returning names where the callable function evaluates to ``True``. An
        example of a valid callable argument would be ``lambda x: x.upper() in
        ['AAA', 'BBB', 'DDD']``. Using this parameter results in much faster
        parsing time and lower memory usage.
    dtype : dtype or dict of {Hashable : dtype}, optional
        Data type(s) to apply to either the whole dataset or individual columns.
        E.g., ``{'a': np.float64, 'b': np.int32, 'c': 'Int64'}``
        Use ``str`` or ``object`` together with suitable ``na_values`` settings
        to preserve and not interpret ``dtype``.
        If ``converters`` are specified, they will be applied INSTEAD
        of ``dtype`` conversion.
    
        .. versionadded:: 1.5.0
    
            Support for ``defaultdict`` was added. Specify a ``defaultdict`` as input where
            the default determines the ``dtype`` of the columns which are not explicitly
            listed.
    engine : {'c', 'python', 'pyarrow'}, optional
        Parser engine to use. The C and pyarrow engines are faster, while the python engine
        is currently more feature-complete. Multithreading is currently only supported by
        the pyarrow engine.
    
        .. versionadded:: 1.4.0
    
            The 'pyarrow' engine was added as an *experimental* engine, and some features
            are unsupported, or may not work correctly, with this engine.
    converters : dict of {Hashable : Callable}, optional
        Functions for converting values in specified columns. Keys can either
        be column labels or column indices.
    true_values : list, optional
        Values to consider as ``True`` in addition to case-insensitive variants of 'True'.
    false_values : list, optional
        Values to consider as ``False`` in addition to case-insensitive variants of 'False'.
    skipinitialspace : bool, default False
        Skip spaces after delimiter.
    skiprows : int, list of int or Callable, optional
        Line numbers to skip (0-indexed) or number of lines to skip (``int``)
        at the start of the file.
    
        If callable, the callable function will be evaluated against the row
        indices, returning ``True`` if the row should be skipped and ``False`` otherwise.
        An example of a valid callable argument would be ``lambda x: x in [0, 2]``.
    skipfooter : int, default 0
        Number of lines at bottom of file to skip (Unsupported with ``engine='c'``).
    nrows : int, optional
        Number of rows of file to read. Useful for reading pieces of large files.
    na_values : Hashable, Iterable of Hashable or dict of {Hashable : Iterable}, optional
        Additional strings to recognize as ``NA``/``NaN``. If ``dict`` passed, specific
        per-column ``NA`` values.  By default the following values are interpreted as
        ``NaN``: " ", "#N/A", "#N/A N/A", "#NA", "-1.#IND", "-1.#QNAN", "-NaN", "-nan",
        "1.#IND", "1.#QNAN", "<NA>", "N/A", "NA", "NULL", "NaN", "None",
        "n/a", "nan", "null ".
    
    keep_default_na : bool, default True
        Whether or not to include the default ``NaN`` values when parsing the data.
        Depending on whether ``na_values`` is passed in, the behavior is as follows:
    
        * If ``keep_default_na`` is ``True``, and ``na_values`` are specified, ``na_values``
          is appended to the default ``NaN`` values used for parsing.
        * If ``keep_default_na`` is ``True``, and ``na_values`` are not specified, only
          the default ``NaN`` values are used for parsing.
        * If ``keep_default_na`` is ``False``, and ``na_values`` are specified, only
          the ``NaN`` values specified ``na_values`` are used for parsing.
        * If ``keep_default_na`` is ``False``, and ``na_values`` are not specified, no
          strings will be parsed as ``NaN``.
    
        Note that if ``na_filter`` is passed in as ``False``, the ``keep_default_na`` and
        ``na_values`` parameters will be ignored.
    na_filter : bool, default True
        Detect missing value markers (empty strings and the value of ``na_values``). In
        data without any ``NA`` values, passing ``na_filter=False`` can improve the
        performance of reading a large file.
    verbose : bool, default False
        Indicate number of ``NA`` values placed in non-numeric columns.
    
        .. deprecated:: 2.2.0
    skip_blank_lines : bool, default True
        If ``True``, skip over blank lines rather than interpreting as ``NaN`` values.
    parse_dates : bool, list of Hashable, list of lists or dict of {Hashable : list}, default False
        The behavior is as follows:
    
        * ``bool``. If ``True`` -> try parsing the index. Note: Automatically set to
          ``True`` if ``date_format`` or ``date_parser`` arguments have been passed.
        * ``list`` of ``int`` or names. e.g. If ``[1, 2, 3]`` -> try parsing columns 1, 2, 3
          each as a separate date column.
        * ``list`` of ``list``. e.g.  If ``[[1, 3]]`` -> combine columns 1 and 3 and parse
          as a single date column. Values are joined with a space before parsing.
        * ``dict``, e.g. ``{'foo' : [1, 3]}`` -> parse columns 1, 3 as date and call
          result 'foo'. Values are joined with a space before parsing.
    
        If a column or index cannot be represented as an array of ``datetime``,
        say because of an unparsable value or a mixture of timezones, the column
        or index will be returned unaltered as an ``object`` data type. For
        non-standard ``datetime`` parsing, use :func:`~pandas.to_datetime` after
        :func:`~pandas.read_csv`.
    
        Note: A fast-path exists for iso8601-formatted dates.
    infer_datetime_format : bool, default False
        If ``True`` and ``parse_dates`` is enabled, pandas will attempt to infer the
        format of the ``datetime`` strings in the columns, and if it can be inferred,
        switch to a faster method of parsing them. In some cases this can increase
        the parsing speed by 5-10x.
    
        .. deprecated:: 2.0.0
            A strict version of this argument is now the default, passing it has no effect.
    
    keep_date_col : bool, default False
        If ``True`` and ``parse_dates`` specifies combining multiple columns then
        keep the original columns.
    date_parser : Callable, optional
        Function to use for converting a sequence of string columns to an array of
        ``datetime`` instances. The default uses ``dateutil.parser.parser`` to do the
        conversion. pandas will try to call ``date_parser`` in three different ways,
        advancing to the next if an exception occurs: 1) Pass one or more arrays
        (as defined by ``parse_dates``) as arguments; 2) concatenate (row-wise) the
        string values from the columns defined by ``parse_dates`` into a single array
        and pass that; and 3) call ``date_parser`` once for each row using one or
        more strings (corresponding to the columns defined by ``parse_dates``) as
        arguments.
    
        .. deprecated:: 2.0.0
           Use ``date_format`` instead, or read in as ``object`` and then apply
           :func:`~pandas.to_datetime` as-needed.
    date_format : str or dict of column -> format, optional
        Format to use for parsing dates when used in conjunction with ``parse_dates``.
        The strftime to parse time, e.g. :const:`"%d/%m/%Y"`. See
        `strftime documentation
        <https://docs.python.org/3/library/datetime.html
        #strftime-and-strptime-behavior>`_ for more information on choices, though
        note that :const:`"%f"` will parse all the way up to nanoseconds.
        You can also pass:
    
        - "ISO8601", to parse any `ISO8601 <https://en.wikipedia.org/wiki/ISO_8601>`_
            time string (not necessarily in exactly the same format);
        - "mixed", to infer the format for each element individually. This is risky,
            and you should probably use it along with `dayfirst`.
    
        .. versionadded:: 2.0.0
    dayfirst : bool, default False
        DD/MM format dates, international and European format.
    cache_dates : bool, default True
        If ``True``, use a cache of unique, converted dates to apply the ``datetime``
        conversion. May produce significant speed-up when parsing duplicate
        date strings, especially ones with timezone offsets.
    
    iterator : bool, default False
        Return ``TextFileReader`` object for iteration or getting chunks with
        ``get_chunk()``.
    chunksize : int, optional
        Number of lines to read from the file per chunk. Passing a value will cause the
        function to return a ``TextFileReader`` object for iteration.
        See the `IO Tools docs
        <https://pandas.pydata.org/pandas-docs/stable/io.html#io-chunking>`_
        for more information on ``iterator`` and ``chunksize``.
    
    compression : str or dict, default 'infer'
        For on-the-fly decompression of on-disk data. If 'infer' and 'filepath_or_buffer' is
        path-like, then detect compression from the following extensions: '.gz',
        '.bz2', '.zip', '.xz', '.zst', '.tar', '.tar.gz', '.tar.xz' or '.tar.bz2'
        (otherwise no compression).
        If using 'zip' or 'tar', the ZIP file must contain only one data file to be read in.
        Set to ``None`` for no decompression.
        Can also be a dict with key ``'method'`` set
        to one of {``'zip'``, ``'gzip'``, ``'bz2'``, ``'zstd'``, ``'xz'``, ``'tar'``} and
        other key-value pairs are forwarded to
        ``zipfile.ZipFile``, ``gzip.GzipFile``,
        ``bz2.BZ2File``, ``zstandard.ZstdDecompressor``, ``lzma.LZMAFile`` or
        ``tarfile.TarFile``, respectively.
        As an example, the following could be passed for Zstandard decompression using a
        custom compression dictionary:
        ``compression={'method': 'zstd', 'dict_data': my_compression_dict}``.
    
        .. versionadded:: 1.5.0
            Added support for `.tar` files.
    
        .. versionchanged:: 1.4.0 Zstandard support.
    
    thousands : str (length 1), optional
        Character acting as the thousands separator in numerical values.
    decimal : str (length 1), default '.'
        Character to recognize as decimal point (e.g., use ',' for European data).
    lineterminator : str (length 1), optional
        Character used to denote a line break. Only valid with C parser.
    quotechar : str (length 1), optional
        Character used to denote the start and end of a quoted item. Quoted
        items can include the ``delimiter`` and it will be ignored.
    quoting : {0 or csv.QUOTE_MINIMAL, 1 or csv.QUOTE_ALL, 2 or csv.QUOTE_NONNUMERIC, 3 or csv.QUOTE_NONE}, default csv.QUOTE_MINIMAL
        Control field quoting behavior per ``csv.QUOTE_*`` constants. Default is
        ``csv.QUOTE_MINIMAL`` (i.e., 0) which implies that only fields containing special
        characters are quoted (e.g., characters defined in ``quotechar``, ``delimiter``,
        or ``lineterminator``.
    doublequote : bool, default True
       When ``quotechar`` is specified and ``quoting`` is not ``QUOTE_NONE``, indicate
       whether or not to interpret two consecutive ``quotechar`` elements INSIDE a
       field as a single ``quotechar`` element.
    escapechar : str (length 1), optional
        Character used to escape other characters.
    comment : str (length 1), optional
        Character indicating that the remainder of line should not be parsed.
        If found at the beginning
        of a line, the line will be ignored altogether. This parameter must be a
        single character. Like empty lines (as long as ``skip_blank_lines=True``),
        fully commented lines are ignored by the parameter ``header`` but not by
        ``skiprows``. For example, if ``comment='#'``, parsing
        ``#empty\na,b,c\n1,2,3`` with ``header=0`` will result in ``'a,b,c'`` being
        treated as the header.
    encoding : str, optional, default 'utf-8'
        Encoding to use for UTF when reading/writing (ex. ``'utf-8'``). `List of Python
        standard encodings
        <https://docs.python.org/3/library/codecs.html#standard-encodings>`_ .
    
    encoding_errors : str, optional, default 'strict'
        How encoding errors are treated. `List of possible values
        <https://docs.python.org/3/library/codecs.html#error-handlers>`_ .
    
        .. versionadded:: 1.3.0
    
    dialect : str or csv.Dialect, optional
        If provided, this parameter will override values (default or not) for the
        following parameters: ``delimiter``, ``doublequote``, ``escapechar``,
        ``skipinitialspace``, ``quotechar``, and ``quoting``. If it is necessary to
        override values, a ``ParserWarning`` will be issued. See ``csv.Dialect``
        documentation for more details.
    on_bad_lines : {'error', 'warn', 'skip'} or Callable, default 'error'
        Specifies what to do upon encountering a bad line (a line with too many fields).
        Allowed values are :
    
        - ``'error'``, raise an Exception when a bad line is encountered.
        - ``'warn'``, raise a warning when a bad line is encountered and skip that line.
        - ``'skip'``, skip bad lines without raising or warning when they are encountered.
    
        .. versionadded:: 1.3.0
    
        .. versionadded:: 1.4.0
    
            - Callable, function with signature
              ``(bad_line: list[str]) -> list[str] | None`` that will process a single
              bad line. ``bad_line`` is a list of strings split by the ``sep``.
              If the function returns ``None``, the bad line will be ignored.
              If the function returns a new ``list`` of strings with more elements than
              expected, a ``ParserWarning`` will be emitted while dropping extra elements.
              Only supported when ``engine='python'``
    
        .. versionchanged:: 2.2.0
    
            - Callable, function with signature
              as described in `pyarrow documentation
              <https://arrow.apache.org/docs/python/generated/pyarrow.csv.ParseOptions.html
              #pyarrow.csv.ParseOptions.invalid_row_handler>`_ when ``engine='pyarrow'``
    
    delim_whitespace : bool, default False
        Specifies whether or not whitespace (e.g. ``' '`` or ``'\t'``) will be
        used as the ``sep`` delimiter. Equivalent to setting ``sep='\s+'``. If this option
        is set to ``True``, nothing should be passed in for the ``delimiter``
        parameter.
    
        .. deprecated:: 2.2.0
            Use ``sep="\s+"`` instead.
    low_memory : bool, default True
        Internally process the file in chunks, resulting in lower memory use
        while parsing, but possibly mixed type inference.  To ensure no mixed
        types either set ``False``, or specify the type with the ``dtype`` parameter.
        Note that the entire file is read into a single :class:`~pandas.DataFrame`
        regardless, use the ``chunksize`` or ``iterator`` parameter to return the data in
        chunks. (Only valid with C parser).
    memory_map : bool, default False
        If a filepath is provided for ``filepath_or_buffer``, map the file object
        directly onto memory and access the data directly from there. Using this
        option can improve performance because there is no longer any I/O overhead.
    float_precision : {'high', 'legacy', 'round_trip'}, optional
        Specifies which converter the C engine should use for floating-point
        values. The options are ``None`` or ``'high'`` for the ordinary converter,
        ``'legacy'`` for the original lower precision pandas converter, and
        ``'round_trip'`` for the round-trip converter.
    
    storage_options : dict, optional
        Extra options that make sense for a particular storage connection, e.g.
        host, port, username, password, etc. For HTTP(S) URLs the key-value pairs
        are forwarded to ``urllib.request.Request`` as header options. For other
        URLs (e.g. starting with "s3://", and "gcs://") the key-value pairs are
        forwarded to ``fsspec.open``. Please see ``fsspec`` and ``urllib`` for more
        details, and for more examples on storage options refer `here
        <https://pandas.pydata.org/docs/user_guide/io.html?
        highlight=storage_options#reading-writing-remote-files>`_.
    
    dtype_backend : {'numpy_nullable', 'pyarrow'}, default 'numpy_nullable'
        Back-end data type applied to the resultant :class:`DataFrame`
        (still experimental). Behaviour is as follows:
    
        * ``"numpy_nullable"``: returns nullable-dtype-backed :class:`DataFrame`
          (default).
        * ``"pyarrow"``: returns pyarrow-backed nullable :class:`ArrowDtype`
          DataFrame.
    
        .. versionadded:: 2.0
    
    Returns
    -------
    DataFrame or TextFileReader
        A comma-separated values (csv) file is returned as two-dimensional
        data structure with labeled axes.
    
    See Also
    --------
    DataFrame.to_csv : Write DataFrame to a comma-separated values (csv) file.
    read_table : Read general delimited file into DataFrame.
    read_fwf : Read a table of fixed-width formatted lines into DataFrame.
    
    Examples
    --------
    >>> pd.read_csv('data.csv')  # doctest: +SKIP
    [31mFile:[39m      c:\users\micha\anaconda3\lib\site-packages\pandas\io\parsers\readers.py
    [31mType:[39m      function



```python
# You aren't limited to just the current folder
macro_data_2 = pd.read_csv('PASTE PATH HERE', index_col=0)
macro_data_2.head()
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[9], line 2
          1 # You aren't limited to just the current folder
    ----> 2 macro_data_2 = pd.read_csv('PASTE PATH HERE', index_col=0)
          3 macro_data_2.head()
    

    File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:1026, in read_csv(filepath_or_buffer, sep, delimiter, header, names, index_col, usecols, dtype, engine, converters, true_values, false_values, skipinitialspace, skiprows, skipfooter, nrows, na_values, keep_default_na, na_filter, verbose, skip_blank_lines, parse_dates, infer_datetime_format, keep_date_col, date_parser, date_format, dayfirst, cache_dates, iterator, chunksize, compression, thousands, decimal, lineterminator, quotechar, quoting, doublequote, escapechar, comment, encoding, encoding_errors, dialect, on_bad_lines, delim_whitespace, low_memory, memory_map, float_precision, storage_options, dtype_backend)
       1013 kwds_defaults = _refine_defaults_read(
       1014     dialect,
       1015     delimiter,
       (...)   1022     dtype_backend=dtype_backend,
       1023 )
       1024 kwds.update(kwds_defaults)
    -> 1026 return _read(filepath_or_buffer, kwds)
    

    File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:620, in _read(filepath_or_buffer, kwds)
        617 _validate_names(kwds.get("names", None))
        619 # Create the parser.
    --> 620 parser = TextFileReader(filepath_or_buffer, **kwds)
        622 if chunksize or iterator:
        623     return parser
    

    File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:1620, in TextFileReader.__init__(self, f, engine, **kwds)
       1617     self.options["has_index_names"] = kwds["has_index_names"]
       1619 self.handles: IOHandles | None = None
    -> 1620 self._engine = self._make_engine(f, self.engine)
    

    File ~\anaconda3\Lib\site-packages\pandas\io\parsers\readers.py:1880, in TextFileReader._make_engine(self, f, engine)
       1878     if "b" not in mode:
       1879         mode += "b"
    -> 1880 self.handles = get_handle(
       1881     f,
       1882     mode,
       1883     encoding=self.options.get("encoding", None),
       1884     compression=self.options.get("compression", None),
       1885     memory_map=self.options.get("memory_map", False),
       1886     is_text=is_text,
       1887     errors=self.options.get("encoding_errors", "strict"),
       1888     storage_options=self.options.get("storage_options", None),
       1889 )
       1890 assert self.handles is not None
       1891 f = self.handles.handle
    

    File ~\anaconda3\Lib\site-packages\pandas\io\common.py:873, in get_handle(path_or_buf, mode, encoding, compression, memory_map, is_text, errors, storage_options)
        868 elif isinstance(handle, str):
        869     # Check whether the filename is to be opened in binary mode.
        870     # Binary mode does not support 'encoding' and 'newline'.
        871     if ioargs.encoding and "b" not in ioargs.mode:
        872         # Encoding
    --> 873         handle = open(
        874             handle,
        875             ioargs.mode,
        876             encoding=ioargs.encoding,
        877             errors=errors,
        878             newline="",
        879         )
        880     else:
        881         # Binary mode
        882         handle = open(handle, ioargs.mode)
    

    FileNotFoundError: [Errno 2] No such file or directory: 'PASTE PATH HERE'



```python
# New useful package!
import os
os.getcwd()
```




    'C:\\Users\\micha\\OneDrive\\Documents\\PhD\\Teaching\\Econ 390 - SP26\\Lecture 11'




```python
# e.g.:
pd.read_csv('macro_data.csv')
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_date</th>
      <th>GDP_PC1</th>
      <th>CPIAUCSL_PC1</th>
      <th>CES0500000003_PC1</th>
      <th>NASDAQCOM_PC1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-01-01</td>
      <td>3.90093</td>
      <td>0.12114</td>
      <td>2.25887</td>
      <td>13.03855</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-01</td>
      <td>2.78707</td>
      <td>1.26736</td>
      <td>2.56214</td>
      <td>0.85409</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2017-01-01</td>
      <td>4.29244</td>
      <td>2.13144</td>
      <td>2.55661</td>
      <td>25.01118</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2018-01-01</td>
      <td>5.32535</td>
      <td>2.43900</td>
      <td>3.01869</td>
      <td>19.09546</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2019-01-01</td>
      <td>4.27694</td>
      <td>1.81326</td>
      <td>3.29920</td>
      <td>6.92507</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2020-01-01</td>
      <td>-0.76462</td>
      <td>1.25294</td>
      <td>4.87856</td>
      <td>28.47922</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2021-01-01</td>
      <td>10.99571</td>
      <td>4.67912</td>
      <td>4.28267</td>
      <td>40.87765</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2022-01-01</td>
      <td>9.81625</td>
      <td>7.99264</td>
      <td>5.37775</td>
      <td>-14.89260</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2023-01-01</td>
      <td>6.74315</td>
      <td>4.12772</td>
      <td>4.44473</td>
      <td>6.04126</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2024-01-01</td>
      <td>5.34489</td>
      <td>2.95161</td>
      <td>4.03304</td>
      <td>32.97673</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2025-01-01</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.90245</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Change the default location!
os.chdir('Wherever You Want it')
macro_data = pd.read_csv('macro_data.csv', index_col=0)
```


    ---------------------------------------------------------------------------

    FileNotFoundError                         Traceback (most recent call last)

    Cell In[12], line 2
          1 # Change the default location!
    ----> 2 os.chdir('Wherever You Want it')
          3 macro_data = pd.read_csv('macro_data.csv', index_col=0)
    

    FileNotFoundError: [WinError 2] The system cannot find the file specified: 'Wherever You Want it'



```python
# Read in from online
macro_data_online = pd.read_csv('http://m-mcmain.github.io/files/Econ390SP26/macro_data.csv', index_col = 'observation_date')
macro_data_online
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>GDP_PC1</th>
      <th>CPIAUCSL_PC1</th>
      <th>CES0500000003_PC1</th>
      <th>NASDAQCOM_PC1</th>
    </tr>
    <tr>
      <th>observation_date</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>2015-01-01</th>
      <td>3.90093</td>
      <td>0.12114</td>
      <td>2.25887</td>
      <td>13.03855</td>
    </tr>
    <tr>
      <th>2016-01-01</th>
      <td>2.78707</td>
      <td>1.26736</td>
      <td>2.56214</td>
      <td>0.85409</td>
    </tr>
    <tr>
      <th>2017-01-01</th>
      <td>4.29244</td>
      <td>2.13144</td>
      <td>2.55661</td>
      <td>25.01118</td>
    </tr>
    <tr>
      <th>2018-01-01</th>
      <td>5.32535</td>
      <td>2.43900</td>
      <td>3.01869</td>
      <td>19.09546</td>
    </tr>
    <tr>
      <th>2019-01-01</th>
      <td>4.27694</td>
      <td>1.81326</td>
      <td>3.29920</td>
      <td>6.92507</td>
    </tr>
    <tr>
      <th>2020-01-01</th>
      <td>-0.76462</td>
      <td>1.25294</td>
      <td>4.87856</td>
      <td>28.47922</td>
    </tr>
    <tr>
      <th>2021-01-01</th>
      <td>10.99571</td>
      <td>4.67912</td>
      <td>4.28267</td>
      <td>40.87765</td>
    </tr>
    <tr>
      <th>2022-01-01</th>
      <td>9.81625</td>
      <td>7.99264</td>
      <td>5.37775</td>
      <td>-14.89260</td>
    </tr>
    <tr>
      <th>2023-01-01</th>
      <td>6.74315</td>
      <td>4.12772</td>
      <td>4.44473</td>
      <td>6.04126</td>
    </tr>
    <tr>
      <th>2024-01-01</th>
      <td>5.34489</td>
      <td>2.95161</td>
      <td>4.03304</td>
      <td>32.97673</td>
    </tr>
    <tr>
      <th>2025-01-01</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>17.90245</td>
    </tr>
  </tbody>
</table>
</div>



## Practice - CSV Files
1. Now, try to *write* the csv file somewhere onto your computer. This is useful when you do datawork and want to export it to use in another program or save to access later. Try using the `to_csv` method on `macro_data_online` with the knowledge you have of `read_csv`.


```python
# Results:
# 1.
macro_data_online.to_csv("macro_data_online.csv")
```

## Excel Files


```python
# You can also read in Excel files
trade = pd.read_excel('trade_data.xlsx')
trade.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>FRED Graph Observations</th>
      <th>Unnamed: 1</th>
      <th>Unnamed: 2</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Federal Reserve Economic Data, Federal Reserve...</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Link: https://fred.stlouisfed.org</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Help: https://fredhelp.stlouisfed.org</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>This data may be copyrighted. Please refer to ...</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>File Created: 2025-12-11 12:04 pm CST</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Specify what sheet you want
trade_quarterly = pd.read_excel('trade_data.xlsx', sheet_name='Quarterly')
trade_quarterly.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_date</th>
      <th>BOPGSTB_PC1</th>
      <th>MRTSSM44000USS_PC1</th>
      <th>DTWEXBGS_PC1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-10-01</td>
      <td>-1.12033</td>
      <td>1.45264</td>
      <td>12.24591</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2016-01-01</td>
      <td>-1.11029</td>
      <td>2.34402</td>
      <td>7.71384</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-04-01</td>
      <td>-1.62633</td>
      <td>1.92334</td>
      <td>4.64050</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-07-01</td>
      <td>-7.21554</td>
      <td>1.84270</td>
      <td>2.21171</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-10-01</td>
      <td>0.89923</td>
      <td>3.28577</td>
      <td>3.93707</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Or columns
exchange_rate_m = pd.read_excel('trade_data.xlsx', sheet_name='Monthly', usecols=[0,3])
exchange_rate_m.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>observation_date</th>
      <th>DTWEXBGS_PC1</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015-11-01</td>
      <td>12.68926</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015-12-01</td>
      <td>11.18015</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2016-01-01</td>
      <td>11.05779</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2016-02-01</td>
      <td>8.66533</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2016-03-01</td>
      <td>4.21801</td>
    </tr>
  </tbody>
</table>
</div>



## Stata Files


```python
# Stata dta files can also be read in!
chilean_SM = pd.read_stata('FUSION_annual_1995.dta')
chilean_SM.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>NUI</th>
      <th>Dvn</th>
      <th>REGION</th>
      <th>CIIU2</th>
      <th>CIIU3</th>
      <th>TAMANO</th>
      <th>ANIO</th>
      <th>FORPRO</th>
      <th>PORNAC</th>
      <th>POREXT</th>
      <th>...</th>
      <th>TOCC</th>
      <th>TOHSC</th>
      <th>TOMSC</th>
      <th>TOSC</th>
      <th>EVTAS</th>
      <th>EVBP</th>
      <th>EVA</th>
      <th>EMPTOT</th>
      <th>VSTK</th>
      <th>avg_sal</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>10082</td>
      <td>K</td>
      <td>2</td>
      <td>3819</td>
      <td>3610</td>
      <td>2</td>
      <td>1995</td>
      <td>1</td>
      <td>100</td>
      <td>0</td>
      <td>...</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>5</td>
      <td>4</td>
      <td>15.0</td>
      <td>85699.0</td>
      <td>1882.666626</td>
    </tr>
    <tr>
      <th>1</th>
      <td>10101</td>
      <td>K</td>
      <td>2</td>
      <td>3721</td>
      <td>2720</td>
      <td>6</td>
      <td>1995</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>452</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>452.0</td>
      <td>216760048.0</td>
      <td>7206.813965</td>
    </tr>
    <tr>
      <th>2</th>
      <td>10103</td>
      <td>6</td>
      <td>2</td>
      <td>3116</td>
      <td>1531</td>
      <td>4</td>
      <td>1995</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>52</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
      <td>8</td>
      <td>6</td>
      <td>52.0</td>
      <td>1567523.0</td>
      <td>4863.653809</td>
    </tr>
    <tr>
      <th>3</th>
      <td>10178</td>
      <td>8</td>
      <td>4</td>
      <td>3114</td>
      <td>1512</td>
      <td>4</td>
      <td>1995</td>
      <td>1</td>
      <td>100</td>
      <td>0</td>
      <td>...</td>
      <td>74</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>6</td>
      <td>4</td>
      <td>74.0</td>
      <td>140901.0</td>
      <td>939.121643</td>
    </tr>
    <tr>
      <th>4</th>
      <td>10220</td>
      <td>2</td>
      <td>5</td>
      <td>3843</td>
      <td>3312</td>
      <td>6</td>
      <td>1995</td>
      <td>2</td>
      <td>0</td>
      <td>100</td>
      <td>...</td>
      <td>496</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>10</td>
      <td>7</td>
      <td>496.0</td>
      <td>10962775.0</td>
      <td>3814.221680</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 378 columns</p>
</div>




```python
# Same with online and specifying the index
chilean_SM_online = pd.read_stata('http://m-mcmain.github.io/files/Econ390SP26/FUSION_annual_1995.dta', index_col = "NUI")
chilean_SM_online.head(5)
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Dvn</th>
      <th>REGION</th>
      <th>CIIU2</th>
      <th>CIIU3</th>
      <th>TAMANO</th>
      <th>ANIO</th>
      <th>FORPRO</th>
      <th>PORNAC</th>
      <th>POREXT</th>
      <th>JORTRA</th>
      <th>...</th>
      <th>TOCC</th>
      <th>TOHSC</th>
      <th>TOMSC</th>
      <th>TOSC</th>
      <th>EVTAS</th>
      <th>EVBP</th>
      <th>EVA</th>
      <th>EMPTOT</th>
      <th>VSTK</th>
      <th>avg_sal</th>
    </tr>
    <tr>
      <th>NUI</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>10082</th>
      <td>K</td>
      <td>2</td>
      <td>3819</td>
      <td>3610</td>
      <td>2</td>
      <td>1995</td>
      <td>1</td>
      <td>100</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>15</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>5</td>
      <td>5</td>
      <td>4</td>
      <td>15.0</td>
      <td>85699.0</td>
      <td>1882.666626</td>
    </tr>
    <tr>
      <th>10101</th>
      <td>K</td>
      <td>2</td>
      <td>3721</td>
      <td>2720</td>
      <td>6</td>
      <td>1995</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>3</td>
      <td>...</td>
      <td>452</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>10</td>
      <td>10</td>
      <td>452.0</td>
      <td>216760048.0</td>
      <td>7206.813965</td>
    </tr>
    <tr>
      <th>10103</th>
      <td>6</td>
      <td>2</td>
      <td>3116</td>
      <td>1531</td>
      <td>4</td>
      <td>1995</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
      <td>...</td>
      <td>52</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>8</td>
      <td>8</td>
      <td>6</td>
      <td>52.0</td>
      <td>1567523.0</td>
      <td>4863.653809</td>
    </tr>
    <tr>
      <th>10178</th>
      <td>8</td>
      <td>4</td>
      <td>3114</td>
      <td>1512</td>
      <td>4</td>
      <td>1995</td>
      <td>1</td>
      <td>100</td>
      <td>0</td>
      <td>2</td>
      <td>...</td>
      <td>74</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>6</td>
      <td>6</td>
      <td>4</td>
      <td>74.0</td>
      <td>140901.0</td>
      <td>939.121643</td>
    </tr>
    <tr>
      <th>10220</th>
      <td>2</td>
      <td>5</td>
      <td>3843</td>
      <td>3312</td>
      <td>6</td>
      <td>1995</td>
      <td>2</td>
      <td>0</td>
      <td>100</td>
      <td>1</td>
      <td>...</td>
      <td>496</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>10</td>
      <td>10</td>
      <td>7</td>
      <td>496.0</td>
      <td>10962775.0</td>
      <td>3814.221680</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 377 columns</p>
</div>



## Practice - Loading Data Online
1. Find a dataset from [WisDOT](https://wisconsindot.gov/Pages/safety/education/crash-data/crashfacts.aspx) and download it manually and read it into Python. Let's avoid reading in any data that was calculated by them (total, average).
2. Now, try to read in the table straight from the website.
3. Are there any columns that would make sense for an index? 


```python
# Results:
# 1.
WisDOT = pd.read_csv('web-county.csv', usecols=range(0,7))
print(WisDOT)
# 2.
WisDOT_online = pd.read_csv('https://wisconsindot.gov/Documents/about-wisdot/newsroom/statistics/crash-fatality/web-county.csv', usecols=range(0,7))
print(WisDOT_online)
# 3.
WisDOT_online = WisDOT_online.set_index('County')
WisDOT_online
```

           County  2026  2025  2024  2023  2022  2021
    0       Adams     0     1     7     8     8     1
    1     Ashland     0     3     1     1     3     1
    2      Barron     0     2    11     7     8     9
    3    Bayfield     0     1     0     2     6     1
    4       Brown     2    10    19    12    14     5
    ..        ...   ...   ...   ...   ...   ...   ...
    68    Waupaca     0     9     3     6     5     9
    69   Waushara     0     5     3     8     3     8
    70  Winnebago     4    12    14    12    11    10
    71       Wood     0     3    12     7     6     6
    72      Total    44   545   576   566   593   593
    
    [73 rows x 7 columns]
           County  2026  2025  2024  2023  2022  2021
    0       Adams     0     1     7     8     8     1
    1     Ashland     0     3     1     1     3     1
    2      Barron     0     2    11     7     8     9
    3    Bayfield     0     1     0     2     6     1
    4       Brown     2    10    19    12    14     5
    ..        ...   ...   ...   ...   ...   ...   ...
    68    Waupaca     0     9     3     6     5     9
    69   Waushara     0     5     3     8     3     8
    70  Winnebago     4    12    14    12    11    10
    71       Wood     0     3    12     7     6     6
    72      Total    44   545   576   566   593   593
    
    [73 rows x 7 columns]
    




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>2026</th>
      <th>2025</th>
      <th>2024</th>
      <th>2023</th>
      <th>2022</th>
      <th>2021</th>
    </tr>
    <tr>
      <th>County</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Adams</th>
      <td>0</td>
      <td>1</td>
      <td>7</td>
      <td>8</td>
      <td>8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Ashland</th>
      <td>0</td>
      <td>3</td>
      <td>1</td>
      <td>1</td>
      <td>3</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Barron</th>
      <td>0</td>
      <td>2</td>
      <td>11</td>
      <td>7</td>
      <td>8</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Bayfield</th>
      <td>0</td>
      <td>1</td>
      <td>0</td>
      <td>2</td>
      <td>6</td>
      <td>1</td>
    </tr>
    <tr>
      <th>Brown</th>
      <td>2</td>
      <td>10</td>
      <td>19</td>
      <td>12</td>
      <td>14</td>
      <td>5</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>Waupaca</th>
      <td>0</td>
      <td>9</td>
      <td>3</td>
      <td>6</td>
      <td>5</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Waushara</th>
      <td>0</td>
      <td>5</td>
      <td>3</td>
      <td>8</td>
      <td>3</td>
      <td>8</td>
    </tr>
    <tr>
      <th>Winnebago</th>
      <td>4</td>
      <td>12</td>
      <td>14</td>
      <td>12</td>
      <td>11</td>
      <td>10</td>
    </tr>
    <tr>
      <th>Wood</th>
      <td>0</td>
      <td>3</td>
      <td>12</td>
      <td>7</td>
      <td>6</td>
      <td>6</td>
    </tr>
    <tr>
      <th>Total</th>
      <td>44</td>
      <td>545</td>
      <td>576</td>
      <td>566</td>
      <td>593</td>
      <td>593</td>
    </tr>
  </tbody>
</table>
<p>73 rows × 6 columns</p>
</div>


