# SPIR-V Multi Validate and LSP

We extended the existing SPIR-V language tooling to allow for exhaustively checking multiple errors
in a compilation unit. We integrated such multi-error checking into a C-API, opening up
possibilities for a semantic LSP similar to clang, for SPIR-V language.

<figure>
  <img
  src="images/2024-spirv-language-ecosystem.jpg"
  alt="The beautiful MDN logo.">
  <figcaption>
      <h4 align="center">
      SPIR-V Ecosystem
      </h4>
  </figcaption>
</figure>

## Background

### SPIR-V Langauge

[`SPIR-V`](https://www.khronos.org/spir/) is an intermediate language targeting graphics and
parallel computing. It is primarily used in Vulkan graphics API and OpenCL. Originally developed as
a dialect of LLVM IR, SPIR-V evolves into its own specification over years. 

SPIR-V streamlines heterogeneous computing by allowing the developers to use any langauge of their choice that compiles into SPIR-V, which is then lowered into vendor-specific implementations. Such process also eliminates the need for proprietary implementations of high-level graphics & compute compilers.


### Hand-Writing SPIR-V

Developers typically do not hand-write SPIR-V, as tools like
[clspv](https://github.com/google/clspv) and 
[glslang](https://github.com/KhronosGroup/glslang)
directly translates higher level heterogeneous languages, such as GLSL, HLSL, and OpenCL C, into SPIR-V. However, sometimes developers hand-write SPIR-V for custom performance tweaking or experimental features.

Hand-writing SPIR-V is challenging due to SPIR-V's IR syntax, and a lack of a real-time syntactic & semantic checking tool; existing toolings provide limited programming aid.

It would best serve low-level graphics & compute programmer, and compiler engineers' interest, to have a real-time LSP for hand-writing SPIR-V code. Before discussing the implementation, first we examine the official toolings provided by the Khronos Group, and the potential challenges engineers face when using them.

### SPIR-V Official Tooling

The Khronos group has implemented 
[SPIRV-Tools](https://github.com/KhronosGroup/SPIRV-Tools). The following three tools from the repo are often used by developers when debugging hand-written SPIR-V: 

`spirv-as` : assembler that turns human-readeable SPIR-V code into SPIR-V binary code; also performs syntax checking when transpiling.

`spirv-dis` : dis-assembler that turns SPIR-V binary code into human-readeable code.

`spirv-val` : a standealone validator that performs semantic checking.

It is worth noting that `spirv-as` and `spirv-val` short-circuits on detecting the first error. So directly writing a frontend LSP that uses the existing C APIs, provides only limited results.

### Third-Party & Community Tooling

[spirv-viewer](https://github.com/daiyousei-qz/spirv-viewer) is a vscode plugin that provides basic syntax highlighting, definition, and documentation on hover. However, it does not perform syntax & semantic checking.  

[vscode-spvasm](https://github.com/PENGUINLIONG/vscode-spvasm) provides similar features using simple, hand-written parsing logic.

## Design

Given the challenges to writing SPIR-V and the status quo of tooling, we seek to implement the following:

1. Expand the `spirv-val` tool to allow for exhaustive error checking, instead of short-circuiting behavior.
2. Integrate the exhaustive error checking in `spirv-val` into a new C API, that interops with arbitrary lsp frontends.

The new features introduced should greatly improve SPIR-V tooling in terms of convenience it provides to the programmers.

## Implementation




## Evaluation


## Future Work


## Summary


## References

[SPIR Overview](https://www.khronos.org/spir/)  
[clspv](https://github.com/google/clspv)  
[glslang](https://github.com/KhronosGroup/glslang)  
[SPIRV-Tools](https://github.com/KhronosGroup/SPIRV-Tools)  
[spirv-viewer](https://github.com/daiyousei-qz/spirv-viewer)  
[vscode-spvasm](https://github.com/PENGUINLIONG/vscode-spvasm)