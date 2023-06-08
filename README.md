# RealityKit-colorLiteral-in-AR-model
How to use #colorLiteral() in RealityKit’s AR model?
# The first part
![IMG_0046](https://github.com/S-way520/RealityKit-colorLiteral-in-AR-model/assets/95877651/b89dbca0-8a2b-4615-b02c-43afafe7a6b7)
# The second part
Code file 1
```swift
import SwiftUI
@main
struct MyApp: App {
    var body: some Scene {
        WindowGroup {
            ContentView()
        }
    }
}
```
Code file 2
```swift
import SwiftUI
import RealityKit
struct ContentView: View {
    var body: some View {
        ZStack{
            ARViewContainer()
                .edgesIgnoringSafeArea(.all)
            Image(systemName: "moonphase.full.moon.inverse")
        }
    }
}
struct ARViewContainer: UIViewRepresentable {
    func makeUIView(context: UIViewRepresentableContext<ARViewContainer>) -> ARView {
        let arView = ARView(frame: .zero, cameraMode: .ar, automaticallyConfigureSession: true)
        let anchorEntity = AnchorEntity(plane: .horizontal)
        arView.tapGesture()
        arView.scene.addAnchor(anchorEntity)
        return arView
    }
    func updateUIView(_ uiView: ARView, context: Context) {}
}
extension ARView{
    func tapGesture() {
        let tapGestureRecognizer = UITapGestureRecognizer(target: self, action: #selector(handleTap(recognizer:)))
        self.addGestureRecognizer(tapGestureRecognizer)
    }
    @objc func handleTap(recognizer: UITapGestureRecognizer) {
        let anchorEntity = AnchorEntity(plane: .horizontal)
        
        let ARentity = ModelEntity(mesh: MeshResource.generateBox(size: 0.2/2, cornerRadius: 0.05/5), materials: [SimpleMaterial(color: UIColor(#colorLiteral(red: 0.23080918192863464, green: 1.0000001192092896, blue: 0.5888275504112244, alpha: 1.0)), isMetallic: true)])//颜色块: #colorLiteral()
        
        ARentity.generateCollisionShapes(recursive: true)
        self.installGestures(.all, for: ARentity)
        anchorEntity.addChild(ARentity)
        self.scene.addAnchor(anchorEntity)
    }
}
```
