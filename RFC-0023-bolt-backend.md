# **RFC0023 for Presto**

See [CONTRIBUTING.md](CONTRIBUTING.md) for instructions on creating your RFC and the process surrounding it.

## Introduce Bolt Backend

Proposers

*
*

## [Related Issues]

N/A

## Summary

Introduce Bolt as a new backend in PrestoDB native execution engine.
To support the Bolt backend, introducing conan as the dependency manager.

## Background

Bolt is a C++ acceleration library providing a composable, extensible, and performant data processing toolkit. It has been validated across multiple frameworks (Spark, Flink, Presto, ElasticSearch), supports diverse processors (x64/ARM CPU, DPU, GPU), and provides access to various storage formats (Parquet, ORC, Text, CSV, Lance) and table management systems (Hive, Paimon) — delivering enterprise-grade cost optimization, result consistency, and feature parity.
Furthermore, integrating Bolt Backend allows reuse of some existing modules and functionalities from the current presto-native-execution.

### Goals

* Support Bolt backend for PrestoDB native execution engine.
* Make behavior easy to switch to the Bolt backend.
* [Nice to have] Modules within presto-native-execution should be shared as much as possible.

## Proposed Implementation

<table>
  <tr>
   <td><strong>Component</strong> 
   </td>
   <td><strong>Shared</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>common</strong> 
   </td>
   <td><strong>No</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>http</strong> 
   </td>
   <td><strong>Yes</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>operators</strong> 
   </td>
   <td><strong>No</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>runtime-metrics</strong> 
   </td>
   <td><strong>Yes</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>tests</strong> 
   </td>
   <td><strong>No</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>thrift</strong> 
   </td>
   <td><strong>Yes</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>types</strong> 
   </td>
   <td><strong>No</strong> 
   </td>
  </tr>
  <tr>
   <td><strong>presto_server_lib</strong> 
   </td>
   <td><strong>No</strong> 
   </td>
  </tr>
</table>

## Adoption Plan

This backend switch is completely transparent to users.

## Test Plan

Unit tests can refer to presto-native-execution/presto_cpp/tests, and additional tests for bolt-related parameter configurations should be added. In addition, some performance benchmark tests (e.g., TPC-DS) are required.