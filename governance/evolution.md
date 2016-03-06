# Evolving the OWIN Specification
## Prelude
This document is intended to provide some additional process around evolving the OWIN standard.

It takes as a starting assumption that the OWIN standard is likely to remain at 1.0, and that additional features subsequent to the 1.0 version of the standard are better defined and ratified as individual features (or groups of features where appropriate) than as modifications to the existing standard requiring the increment of a monolithic standard version.

### Capability over Compatibility
It is suggested that allowing additional features to be adopted individually by server implementations (and potentially "polyfilled" by library implementations) is more practical given the software landscape than requiring a server to implement all of a standard to achieve a binary yes/no compatibility.

In this sense, server implementations may choose to implement features piecemeal, and should advertise/document capabilities instead of claiming compatibility (excluding the base 1.0.x specification, which is taken to be an immutable baseline).

### Governance

This process is intended to lead to an evolutionary change in OWIN over time, requiring less governance overhead as the impact of an addition is minimized by it being an isolated change with an obvious scope. The process for voting/ratifying an evolutionary change of this type may be able to be lighter than the existing process for agreeing an update to the monolithic specification (although the existing voting procedure is not suggested to change as part of this proposal).

## Implementation

It is proposed that the existing 1.0.x OWIN standard becomes the final baseline standard, and any new changes conform to a lighter process designed to ensure isolation and minimization of impact.

__For each change:__

An __OWIN Extension__ is created and assigned a number (a simple increasing count can be used). For example, the existing proposal to add "server.OnInit" and "server.OnDispose" items to the OWIN Environment would be created as OWIN Extension 1.

Each Extension is created in a Proposal state, and may be discussed and voted on to reach Candidate state. When two independent implementations of an Extension in Candidate state exist, it will have Candidate status removed, and become a simple Extension, accepted as part of the OWIN standards base.

It is expected that consumers of server implementations SHOULD determine whether a specific extension is supported by inspecting the keys present, which should be defined as part of the Extension.

*Servers implementing an Extension MAY choose to signal the implementation by using the existing "server.Capabilities" functionality defined as part of the OWIN Common Keys documentation, though this is not part of the core OWIN specification. In contrast with the featurename.Version key (and potential detail value) expected for extension support, it should be sufficient to signal binary support for an OWIN Extension by adding a key "extension.<number>" giving the appropriate value. A server wishing to indicate that "server.OnInit" and "server.OnDispose" are supported would add "extension.1" to the "server.Capabilities" dictionary.*

Servers should NOT distinguish between different states of an Extension.

## Requirements

Where possible, new Extensions *should* give details of how the feature could be polyfilled for existing implementations (although this may not always be possible). This requirement is in addition to the common requirements of rationale and design thinking expected for any proposal to extend a standard.

## Next Steps

Outstanding decisions to be formulated as OWIN Extensions in Proposal state and processed via the existing voting process.

