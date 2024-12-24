<ul>
<li><p>쿼터니언</p>
<ul>
<li>Vector3로만 회전을 나타내면 짐벌락이라는 현상이 발생한다</li>
<li>이를 보완하기 위해 가상의 공간을 하나 더 만들어 Vector4로 회전을 계산한다</li>
</ul>
</li>
<li><p>짐벌락</p>
<ul>
<li>x,y,z축을 이용하여 회전을 할 때 축이 겹쳐지게 되면서 회전이 발생하지 않는 현상을 말한다</li>
</ul>
</li>
<li><p>bool Matrix::Decompose(Vector3&amp; scale, Quaternion&amp; rotation, Vector3&amp; translation)</p>
<ul>
<li>Matrix로 만든 것을 역으로 분해 SRT로 분해해주는 함수</li>
</ul>
</li>
<li><p>Component</p>
<ul>
<li>기본 부품들을 추가해 GameObject 클래스에서 조립을 하여 가지고 있게끔 하는 클래스이다</li>
</ul>
</li>
<li><p>Transform</p>
<ul>
<li>이 클래스에서는 수학 시간에 배웠던 것을 토대로 SRT를 행렬로 만들어 스자이공부를 적용하여 연산을 하게 만들 것이므로 Component 클래스를 상속받아 만들어준다</li>
<li>SetScale, SetRotation, SetPosition<ul>
<li>SetScale, SetRotation, SetPosition은 각각의 값을 입력받아 Local에 있는 SRT를 설정해 주는 함수들이지만 parent가 존재하면 world가 아닌 parent에 영향을 받아 값이 값이 변할 수 있도록 해준다<ul>
<li>SetRotation, SetPosition에서 Parent가 존재할 때 Parent의 Matrix의 역행렬을 가져와 연산하는 이유는 Parent의 Matrix로 연산을 하면 부모에서 World로 가는 변환행렬을 연산하는 것이므로 부모에서 자식으로 가는 변환행렬을 계산해야 하므로 역행렬을 구해 연산해야 한다</li>
</ul>
</li>
</ul>
</li>
<li>UpdateTransform<ul>
<li>UpdateTransform 함수에서는 localScale, localRotation, localPosition을 각각 행렬로 만들어준 뒤 3개의 값을 곱해 SRT가 들어간 4x4행렬을 만들어준다</li>
<li>그 후 Parent가 있다면 구한 local 행렬과 Parent의 World행렬을 곱해 matWorld에 저장하고, 그렇지 않으면 local 행렬을 저장해주어 각각의 물체에 World 행렬을 지정해준다</li>
<li>이때 회전을 3차원 공간에서 하게되면 짐벌락이라는 현상이 발생하므로 쿼터니언을 이용해 회전처리를 한 뒤 오일러 회전을 하게 끔 만들어 주어야 한다</li>
<li>이렇게 구한 SRT를 이용해 X,Y,Z축인 right, up, look 변수에 TransformNormal 함수를 이용해 World상에서 변화가 일어날 수 있게 만들어준다</li>
<li>마지막으로 Parent가 아닌 children이 존재한다면 그 값들 모두 변할 수 있게 for each문을 통해 UpdateTransform 함수를 콜해준다다</li>
</ul>
</li>
</ul>
</li>
</ul>
<pre><code class="language-cpp">//Local
Vec3 GetLocalScale() { return localScale; }
Vec3 GetLocalRotation() { return localRotation; }
Vec3 GetLocalPosition() { return localPosition; }

//World
Vec3 GetScale() { return scale; }
Vec3 GetRotation() { return rotation; }
Vec3 GetPosition() { return position; }

Matrix GetWorldMatrix() { return matWorld; }

//계층 관계
bool HasParnet() { return parent != nullptr; }
shared_ptr&lt;Transform&gt; GetParent() { return parent; }
void SetParent(shared_ptr&lt;Transform&gt; Parent) { parent = Parent; }

const vector&lt;shared_ptr&lt;Transform&gt;&gt;&amp; GetChildren() { return children; }
void AddChild(shared_ptr&lt;Transform&gt; Child) { children.push_back(Child); }

...

Vec3 Transform::ToEulerAngles(Quaternion q)
{
    Vec3 angles;

    // roll (x-axis rotation)
    double sinr_cosp = 2 * (q.w * q.x + q.y * q.z);
    double cosr_cosp = 1 - 2 * (q.x * q.x + q.y * q.y);
    angles.x = std::atan2(sinr_cosp, cosr_cosp);

    // pitch (y-axis rotation)
    double sinp = std::sqrt(1 + 2 * (q.w * q.y - q.x * q.z));
    double cosp = std::sqrt(1 - 2 * (q.w * q.y - q.x * q.z));
    angles.y = 2 * std::atan2(sinp, cosp) - 3.14159f / 2;

    // yaw (z-axis rotation)
    double siny_cosp = 2 * (q.w * q.z + q.x * q.y);
    double cosy_cosp = 1 - 2 * (q.y * q.y + q.z * q.z);
    angles.z = std::atan2(siny_cosp, cosy_cosp);

    return angles;
}

void Transform::UpdateTransform()
{
    Matrix matscale = Matrix::CreateScale(localScale);
    Matrix matrotation = Matrix::CreateRotationX(localRotation.x);
    matrotation *= Matrix::CreateRotationY(localRotation.y);
    matrotation *= Matrix::CreateRotationZ(localRotation.z);
    Matrix mattranslation = Matrix::CreateTranslation(localPosition);

    matLocal = matscale * matrotation * mattranslation;

    if (HasParnet() == true)
        matWorld = matLocal * parent-&gt;GetWorldMatrix();
    else
        matWorld = matLocal;

    Quaternion quat;
    matWorld.Decompose(scale, quat, position);
    rotation = ToEulerAngles(quat);

    right = Vec3::TransformNormal(Vec3::Right, matWorld);
    up = Vec3::TransformNormal(Vec3::Up, matWorld);
    look = Vec3::TransformNormal(Vec3::Backward, matWorld);
    //Dx에서 왼존 좌표계를 사용하지만 SimpleMath는 오른손 좌표계로 만들어져 있어 Forward가 아닌 Backward를 사용함

    //Children
    for (const shared_ptr&lt;Transform&gt;&amp; c : children)
        c-&gt;UpdateTransform();
}

void Transform::SetLocalScale(const Vec3&amp; Scale)
{
    localScale = Scale;
    UpdateTransform();
}

void Transform::SetLocalRotation(const Vec3&amp; Rotation)
{
    localRotation = Rotation;
    UpdateTransform();
}

void Transform::SetLocalPosition(const Vec3&amp; Position)
{
    localPosition = Position;
    UpdateTransform();
}

void Transform::SetScale(const Vec3&amp; Scale)
{
    if (HasParnet() == true)
    {
        Vec3 parentScale = parent-&gt;GetScale();
        Vec3 tempScale = Scale;
        tempScale.x /= parentScale.x;
        tempScale.y /= parentScale.y;
        tempScale.z /= parentScale.z;

        SetLocalScale(tempScale);
    }
    else
        SetLocalScale(Scale);
}

void Transform::SetRotation(const Vec3&amp; Rotation)
{
    if (HasParnet() == true)
    {
        Matrix worldToParentLocalMatrix = parent-&gt;GetWorldMatrix().Invert();

        Vec3 tempRotation;
        tempRotation.Transform(Rotation, worldToParentLocalMatrix);
        SetLocalRotation(tempRotation);
    }
    else
        SetLocalRotation(Rotation);
}

void Transform::SetPosition(const Vec3&amp; Position)
{
    if (HasParnet() == true)
    {
        //부모의 local에서 world로 가는 변환 행렬의 역행렬을 구하면 월드 좌표계를 기준으로 존재한 좌표를
        //부모좌표계를 기준으로 좌표를 변환할 수 있다
        Matrix worldToParentLocalMatrix = parent-&gt;GetWorldMatrix().Invert();

        Vec3 tempPosition;
        tempPosition.Transform(Position, worldToParentLocalMatrix);
        SetLocalPosition(tempPosition);
    }
    else
        SetLocalPosition(Position);
}
</code></pre>
<ul>
<li>GameObject<ul>
<li>GameObject클래스의 Update 함수에서 물체들이 변하는 것을 Transform 클래스로 옮겼으므로 Transform 객체를 만들어 Update함수에서는 변화할 값을 Transform으로 넘겨주게 해주도록 변경해주면 SRT 변화가 잘 일어난다</li>
</ul>
</li>
</ul>
<pre><code class="language-cpp">void GameObject::Update()
{
    //Vec3 pos = transform-&gt;GetPosition();
    //pos.x += 0.001f;
    //transform-&gt;SetPosition(pos);

    Vec3 pos = parent-&gt;GetPosition();
    pos.x += 0.001f;
    parent-&gt;SetPosition(pos);
    Vec3 rot = parent-&gt;GetRotation();
    rot.z += 0.001f;
    parent-&gt;SetRotation(rot);

    transformData.World = transform-&gt;GetWorldMatrix();

    constantBuffer-&gt;CopyData(transformData);
}
</code></pre>