---
source: sources/wiki-Apache_Avro.md
source_url: https://en.wikipedia.org/wiki/Apache_Avro
---

## Apache Avro: Schema-Based Data Serialization and RPC Framework

Apache Avro is a row-oriented remote procedure call and data serialization framework developed within the Apache Hadoop ecosystem. It uses JSON to define data types and protocols, serializes data in a compact binary format, and is distinguished from similar frameworks (Thrift, Protocol Buffers) by its ability to handle schema changes without requiring code regeneration. Avro serves as both a persistent data serialization format and a wire format for inter-node communication in Hadoop clusters.

## Key Concepts

- **Row-oriented serialization**: Avro serializes data row-by-row, in contrast to column-oriented formats like Parquet or ORC
- **Schema-driven**: All data is structured according to a schema; the schema can be embedded with the data so readers don't need to know it ahead of time
- **Two schema languages**: Avro IDL (human-friendly, C-like syntax) and JSON-based schema (machine-readable)
- **No code generation required**: Unlike Thrift and Protocol Buffers, Avro does not require a code-generation step when schemas change (though code generation is available for statically-typed languages)
- **Primitive types**: null, boolean, int, long, float, double, bytes, string
- **Complex types**: record, enum, array, map, union, fixed
- **Two serialization encodings**: binary (compact, fast, default for production) and JSON (used for debugging and web applications)
- **Schema embedded in data files**: Avro Object Container Files carry their schema, enabling self-describing data
- **Union types for nullable fields**: Fields like `["null", "int"]` express optional values — this is Avro's mechanism for nullable fields

## Commands and Syntax

**Schema definition (JSON)**:
```json
{
  "namespace": "example.avro",
  "type": "record",
  "name": "User",
  "fields": [
    {"name": "name", "type": "string"},
    {"name": "favorite_number", "type": ["null", "int"]},
    {"name": "favorite_color", "type": ["null", "string"]}
  ]
}
```

**Python serialization**:
```python
import avro.schema
from avro.datafile import DataFileWriter
from avro.io import DatumWriter

schema = avro.schema.parse(open("user.avsc", "rb").read())
writer = DataFileWriter(open("users.avro", "wb"), DatumWriter(), schema)
writer.append({"name": "Alyssa", "favorite_number": 256})
writer.close()
```

**Python deserialization** (schema is read from the file):
```python
from avro.datafile import DataFileReader
from avro.io import DatumReader

reader = DataFileReader(open("users.avro", "rb"), DatumReader())
for user in reader:
    print(user)
reader.close()
```

**Object Container File structure**:
1. File header: magic bytes (`Obj\x01`), file metadata (including schema), 16-byte random sync marker
2. One or more data blocks containing serialized records

## Relationships

- **Apache Hadoop**: Avro was developed within the Hadoop project; serves as Hadoop's native serialization and RPC wire format
- **Thrift and Protocol Buffers**: Direct competitors; key differentiator is Avro's dynamic schema resolution without mandatory code generation
- **Apache Spark SQL**: Can read Avro as a data source natively
- **Parquet/ORC**: Complementary column-oriented formats; Avro is row-oriented, better suited for write-heavy workloads and record-at-a-time processing; Parquet/ORC better for analytical queries
- **Schema Registry** (e.g., Confluent): Often used with Kafka to manage Avro schema evolution
- **Schema evolution**: Avro's design supports forward and backward compatibility — readers and writers can use different but compatible schema versions

## Exam-Relevant Points

- Avro is **row-oriented**, not column-oriented — contrast with Parquet (columnar)
- Avro **does not require code generation** for schema changes, unlike Thrift and Protocol Buffers
- Schemas are defined in **JSON** (or Avro IDL); data is serialized in **compact binary**
- Avro Object Container Files are **self-describing**: they embed the writer's schema in the file header
- The file header magic bytes are `Obj` followed by version `1` (hex: `4F 62 6A 01`)
- Avro supports both **serialization** (persistent data storage) and **RPC** (wire protocol for communication)
- Union types (e.g., `["null", "int"]`) are the mechanism for **nullable/optional fields**
- The 16-byte **sync marker** in the file header enables splitting large files for parallel processing in MapReduce
- Licensed under **Apache License 2.0**; APIs exist for 14+ languages including Java, Python, C, Go, and Rust
