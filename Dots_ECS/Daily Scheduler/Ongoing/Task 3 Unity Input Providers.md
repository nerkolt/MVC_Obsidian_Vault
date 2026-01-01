### Phase 1: UnityLegacyInputProvider

- [x] Create `UnityLegacyInputProvider.cs` component struct
- [x] Create `UnityLegacyInputConfiguration.cs` managed companion
- [x] Create `UnityLegacyInputProviderAuthoring.cs` with axis name fields
- [x] Create `UnityLegacyInputProviderBaker.cs`
- [x] Create `UnityLegacyInputProviderSystem.cs`
- [ ] Test with sample vehicle

* All three implement the same **`IInputProvider`** interface, so vehicles don't care which one you use.