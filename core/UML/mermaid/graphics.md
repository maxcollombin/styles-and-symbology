# Graphics

```mermaid
  classDiagram
  %% Class definition
    class Graphic {
        opacity: float
        transform: Transform2D
        transform3D: Transform3D
    }
    class Shape {
        stroke: Stroke [0..1]
    }
    class ClosedShape {
        fill: Fill [0..1]
    }
    class Dot {
        point: Pointf
    }
    class Rectangle {
       topLeft: Pointf
       bottomRight: Pointf
    }
    class RoundedRectangle {
        rx: float
        ry: float
    }
    class Circle {
        center: Pointf
        radius: float
    }
    class Ellipse {
        center: Pointf
        radiusX: float
        radiusY: float
    }
    class ClosedArcType {
       <<enumeration>>
       sector
       chord
    }

    class ClosedArc {
        type: ClosedArcType
    }

    class Arc {
        center: Pointf
        radius: float
        innerRadius: float
        startAngle: Angle
        deltaAngle: Angle
    }
    class PathNodes {
       points: Pointf[*]
    }
    class ClosedPath {
        innerNodes: PathNodes[0..*]
    }

    class Path {
        nodes: PathNodes
    }
    class TextAlignment {
      horizontal: HAlignment
      vertical: VAlignment
    }
    class HAlignment {
      <<enumeration>>
      left
      center
      right
    }
    class VAlignment {
      <<enumeration>>
      top
      middle
      bottom
    }
    class FontOutline {
       size: float
       opacity: float
       color: Color
    }
    class Font {
      face: string
      size: float
      bold: bool
      italic: bool
      underline: bool
      color: Color
      opacity: float
      outline: FontOutline
    }

    class Text {
        text: string
        font: Font
        alignment: TextAlignment
    }
    class Resource {
       path: string[0..1] -- local file resources
       url: string[0..1] -- online resources
       id: string[0..1] -- resources in DB tables or within a srite
       type: string[0..1] -- identify the media type the resource is available in
       ext: string[0..1] -- build paths or URLs from id and extensions
       sprite: string[0..1] -- name of sprite file e.g., with Mapbox GL styles
    }
    class Image {
        image: Resource
        hotSpot: Pointf
        tint: Color
        blackTint: Color
        alphaThreshold: float
    }
    class Model {
        model: Resource
    }
    class MultiGraphic {
        elements: Graphic [*]
    }
    class GraphicInstance {
       element: Graphic
    }
    class Vector3D {
       x: double
       y: double
       z: double
    }
    class Vector3Df {
       x: float
       y: float
       z: float
    }
    class Quaternion {
       x: double
       y: double
       z: double
       w: double
    }
    class Transform3D {
        orientation: Quaternion
        position: Vector3D
        scaling: Vector3Df
    }
    class Transform2D {
        rotationScaling: float [4]
        translation: Pointf
    }
    class Pointf {
        x: float
        y: float
    }

    class Color {
      r: float
      g: float
      b: float
    }
    class Gradient {
        colorKeys: ColorKey [*]
    }
    class ColorKey {
      color: Color
      opacity: float
      percent: float
    }
    class StippleStyle {
      <<enumeration>>
      light
      medium
      heavy
    }
    class HatchStyle {
      <<enumeration>>
      forward
      backward
      xCross
      cross
    }
    class StrokeJoin {
      <<enumeration>>
      miter
      round
      bevel
    }
    class StrokeCap {
      <<enumeration>>
      butt
      round
      square
    }
    class Fill {
      pattern: Graphic [0..1]
      color: Color
      stippleStyle: StippleStyle
      hatchStyle: HatchStyle
      gradient: Gradient
    }
    class GraphicalUnit {
       <<enumeration>>
       pixels
       meters
       feet
       percent
       points
       em
       screenInches
       screenCM
       screenMM
    }
    class StrokeStyling {
       color: Color
       opacity: float
       width: float
       widthUnit: GraphicalUnit
    }
    class Stroke {
      pattern: Graphic [0..1]
      center: StrokeStyling [0..1]
      casing: StrokeStyling [0..1]
      join: StrokeJoin [0..1]
      cap: StrokeCap [0..1]
      dashPattern: integer [*]
    }

  %% Relations
  %% Inheritance
  Text --|> Graphic
  Image --|> Graphic
  MultiGraphic --|> Graphic
  Dot --|> Shape
  Shape --|> Graphic
  Rectangle --|> ClosedShape
  Circle --|> ClosedShape
  Ellipse --|>Closed Shape
  Arc --|> Shape
  ClosedArc --|> Arc
  ClosedArc --|> ClosedShape
  Path --|> Shape
  RoundedRectangle --|> Rectangle
  GraphicInstance --|> Graphic
  Stroke --|> StrokeStyling
  Model --|> Graphic
  ClosedPath --|> Path
  ClosedPath --|> ClosedShape
  ClosedShape --|> Shape

  %% Composition
  PathNodes --* Pointf
  ClosedPath --* PathNodes
  Path --* PathNodes
  Dot --* Pointf
  Circle --* Pointf
  Ellipse --* Pointf
  Rectangle --* Pointf
  Arc --* Pointf
  ClosedArc --* ClosedArcType
  Graphic --* Transform2D
  Graphic --* Transform3D
  Transform3D --* Quaternion
  Transform3D --* Vector3D
  Transform3D --* Vector3Df
  Transform2D --* Pointf
  Image --* Resource
  Image --* Color
  Image --* Pointf
  Model --* Resource
  MultiGraphic --* Graphic
  Text --* Font
  Text --* TextAlignment
  Font --* FontOutline
  Font --* Color
  FontOutline --* Color
  TextAlignment --* HAlignment
  TextAlignment --* VAlignment
  ClosedShape --* Fill
  Shape --* Stroke

  Fill --* Graphic
  Fill --* Color
  Fill --* Gradient
  Fill --* HatchStyle
  Fill --* StippleStyle
  ColorKey --* Color
  Gradient --* ColorKey
  StrokeStyling --* Color
  StrokeStyling --* GraphicalUnit
  Stroke --* Graphic
  Stroke --* StrokeStyling
  Stroke --* StrokeJoin
  Stroke --* StrokeCap

  %% Aggregation
  GraphicInstance --o Graphic

```