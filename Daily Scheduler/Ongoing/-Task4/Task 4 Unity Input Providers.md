### Phase 1: MVC Core Infrastructure

**Core Components (3 files):**
- [ ] Create `PlayerIdentifier` IComponentData in `Vehicles/Runtime/Core/`
- [ ] Create `PlayerIdentifierAuthoring` MonoBehaviour
- [ ] Create `PlayerIdentifierBaker` (ECS + MonoBaker)

**Input Providers (3 files):**
- [ ] Create `PluginInputProvider` abstract class
- [ ] Create `VehicleInputSettings` ScriptableSingleton
- [ ] Create `PluginInputBootstrapper` initialization class
- [ ] Create `PluginInputReaderSystem` SystemBase

---
### Phase 2: Plugin Implementations

**InputsManager Plugin (1 file):**
- [ ] Create `InputsManagerProvider` extending `PluginInputProvider`
- [ ] Integrate with existing InputsManager infrastructure

**Legacy Input Plugin (1 file):**
- [ ] Create `LegacyInputProvider` extending `PluginInputProvider`
- [ ] Configure axis names for Unity Input Manager

**New Input System Plugin (1 file):**
- [ ] Create `InputSystemProvider` extending `PluginInputProvider`
- [ ] Add `versionDefines` for `ENABLE_INPUT_SYSTEM`
- [ ] Configure InputActionReferences

---
### Phase 3: Testing & Validation

**Functional Tests:**
- [ ] Test split-screen with multiple players
- [ ] Test different GearShiftControlType configurations
- [ ] Verify plugin discovery via reflection
- [ ] Test ECS and GameObject execution modes

**Integration Tests:**
- [ ] Verify `PluginInputReaderSystem` writes to `Powertrain.Inputs`
- [ ] Test plugin switching via `VehicleInputSettings`

---