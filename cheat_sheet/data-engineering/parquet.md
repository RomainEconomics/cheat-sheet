# Parquet

[Greate Explanation](https://vutr.substack.com/p/the-overview-of-parquet-file-format)

- Parquet groups data into `row groups` each containing a subset of rows. (**horizontal partition**)
- Within each row group, data for each column is called a `column chunk.` (**vertical partition**)

In the row group, these chunks are guaranteed to be stored contiguously on disk.

Parquet organizes data in a hybrid format, and thus is not strictly a "column oriented"

A Parquet file is composed of:

- **Row Groups**: Each row group contains a subset of the rows in the dataset. Data is organized into columns within each row group, each stored in a column chunk. Each row group has a header.j
- **Column Chunk:** A chunk is the data for a particular column in the row group.
- **Pages**: Column chunk is further divided into pages. A page is the smallest data unit in Parquet. There are several types of pages, including data pages (which contain the actual data), dictionary pages (which contain dictionary-encoded values), and index pages (used for faster data lookup).

Parquet is a self-described file format that contains all the information needed for the application that consumes the file.
This allows the software to efficiently understand and process the file without requiring external information.

Thus, the metadata is the crucial part of Parquet.
