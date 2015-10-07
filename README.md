# bombermine-assets

Advanced asset manager for bombermine with entity-component architecture

This repository will contain basic implementation and tests.

## design

1. asset is constructed from JSON description
2. every asset has a number of components
3. component can reference other asset. in that case, asset cant be loaded before the other asset.
4. component can contain subassets
5. subassets reference is "parentAsset.childAsset"
6. type of components:
    * single texture
    * multiple textures
    * single frame in texture
    * multiple frames in texture (for simple single-page atlas)
    * bombermine skin
    * bombermine constructor type (pony, human, hamster, e.t.c.)
    * spine atlas
    * spine skeleton

7. two implementations:
  ```java 
  class Asset extends Disposable {
  	List<AssetComponent> components;
  	Frame frame;
  	Texture texture;
  	List<Texture> textures;
  	BombermineSkin skin;
  	SpineAtlas spineAtlas;
  	SpineData spineSkeleton;
  }
  class AssetComponent extends Disposable {
  }
  ```
  
  ```javascript
  Asset.prototype = { lalala : "lalala" }
  ```

9. multiple middlewares analyze description (which is json object) and construct components IN PARTICULAR ORDER

10. there are two type of lists of assets - static and dynamic.

11. disposing of dynamic asset means that NO ONE IS USING IT IN THE SCENE, also asset cant be disposed if some other asset component references it. If only child references it, its not a problem. There are no circular references.
